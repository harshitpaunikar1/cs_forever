Title: file-journaling.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/file-journaling.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:33+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

42
Crash Consistency: FSCK and Journaling
As we’ve seen thus far, the ﬁle system manages a set of data struc tures to
implement the expected abstractions: ﬁles, directories, and all of the other
metadata needed to support the basic abstraction that we expec t from a
ﬁle system. Unlike most data structures (for example, those foun d in
memory of a running program), ﬁle system data structures must persist,
i.e., they must survive over the long haul, stored on devices that retain
data despite power loss (such as hard disks or ﬂash-based SSDs).
One major challenge faced by a ﬁle system is how to update persis -
tent data structures despite the presence of a power loss or system crash.
Speciﬁcally , what happens if, right in the middle of updating on -disk
structures, someone trips over the power cord and the machine loses
power? Or the operating system encounters a bug and crashes? Bec ause
of power losses and crashes, updating a persistent data structu re can be
quite tricky , and leads to a new and interesting problem in ﬁle system
implementation, known as the crash-consistency problem.
This problem is quite simple to understand. Imagine you have to up-
date two on-disk structures, A and B, in order to complete a particular
operation. Because the disk only services a single request at a t ime, one
of these requests will reach the disk ﬁrst (either A or B). If the system
crashes or loses power after one write completes, the on-disk struc ture
will be left in an inconsistent state. And thus, we have a problem that all
ﬁle systems need to solve:
THE CRUX : H OW TO UPDATE THE DISK DESPITE CRASHES
The system may crash or lose power between any two writes, and
thus the on-disk state may only partially get updated. After th e crash,
the system boots and wishes to mount the ﬁle system again (in order to
access ﬁles and such). Given that crashes can occur at arbitra ry points
in time, how do we ensure the ﬁle system keeps the on-disk image i n a
reasonable state?
1

2 C RASH CONSISTENCY : FSCK AND JOURNALING
In this chapter, we’ll describe this problem in more detail, and look
at some methods ﬁle systems have used to overcome it. We’ll begin by
examining the approach taken by older ﬁle systems, known as fsck or the
ﬁle system checker . We’ll then turn our attention to another approach,
known as journaling (also known as write-ahead logging ), a technique
which adds a little bit of overhead to each write but recovers more quickly
from crashes or power losses. We will discuss the basic machinery of
journaling, including a few different ﬂavors of journaling that Linux ext3
[T98,PAA05] (a relatively modern journaling ﬁle system) impl ements.
42.1 A Detailed Example
To kick off our investigation of journaling, let’s look at an example.
We’ll need to use a workload that updates on-disk structures in some
way . Assume here that the workload is simple: the append of a sing le
data block to an existing ﬁle. The append is accomplished by open ing the
ﬁle, calling lseek() to move the ﬁle offset to the end of the ﬁle, and then
issuing a single 4KB write to the ﬁle before closing it.
Let’s also assume we are using standard simple ﬁle system stru ctures
on the disk, similar to ﬁle systems we have seen before. This tin y example
includes an inode bitmap (with just 8 bits, one per inode), a data bitmap
(also 8 bits, one per data block), inodes (8 total, numbered 0 to 7, and
spread across four blocks), and data blocks (8 total, numbered 0 to 7).
Here is a diagram of this ﬁle system:
Bitmaps
Inode Data Inodes Data BlocksI[v1] Da
0 1 2 3 4 5 6 7 0 1 2 3 4 5 6 7
If you look at the structures in the picture, you can see that a sing le inode
is allocated (inode number 2), which is marked in the inode bitma p, and a
single allocated data block (data block 4), also marked in the da ta bitmap.
The inode is denoted I[v1], as it is the ﬁrst version of this inode; i t will
soon be updated (due to the workload described above).
Let’s peek inside this simpliﬁed inode too. Inside of I[v1], we see :
owner : remzi
permissions : read-write
size : 1
pointer : 4
pointer : null
pointer : null
pointer : null
In this simpliﬁed inode, the size of the ﬁle is 1 (it has one block al-
located), the ﬁrst direct pointer points to block 4 (the ﬁrst data block of
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

CRASH CONSISTENCY : FSCK AND JOURNALING 3
the ﬁle, Da), and all three other direct pointers are set to null (indicating
that they are not used). Of course, real inodes have many more ﬁeld s; see
previous chapters for more information.
When we append to the ﬁle, we are adding a new data block to it, an d
thus must update three on-disk structures: the inode (which mu st point
to the new block and record the new larger size due to the append) , the
new data block Db, and a new version of the data bitmap (call it B[v 2]) to
indicate that the new data block has been allocated.
Thus, in the memory of the system, we have three blocks which we
must write to disk. The updated inode (inode version 2, or I[v2] for short)
now looks like this:
owner : remzi
permissions : read-write
size : 2
pointer : 4
pointer : 5
pointer : null
pointer : null
The updated data bitmap (B[v2]) now looks like this: 00001100. F inally ,
there is the data block (Db), which is just ﬁlled with whatever it is users
put into ﬁles. Stolen music, perhaps?
What we would like is for the ﬁnal on-disk image of the ﬁle system to
look like this:
Bitmaps
Inode Data Inodes Data BlocksI[v2] Da Db
0 1 2 3 4 5 6 7 0 1 2 3 4 5 6 7
To achieve this transition, the ﬁle system must perform three s epa-
rate writes to the disk, one each for the inode (I[v2]), bitmap (B [v2]), and
data block (Db). Note that these writes usually don’t happen imme di-
ately when the user issues a write() system call; rather, the dirty in-
ode, bitmap, and new data will sit in main memory (in the page cache
or buffer cache ) for some time ﬁrst; then, when the ﬁle system ﬁnally
decides to write them to disk (after say 5 seconds or 30 seconds), the ﬁle
system will issue the requisite write requests to the disk. U nfortunately ,
a crash may occur and thus interfere with these updates to the d isk. In
particular, if a crash happens after one or two of these writes ha ve taken
place, but not all three, the ﬁle system could be left in a funny s tate.
Crash Scenarios
To understand the problem better, let’s look at some example crash sce-
narios. Imagine only a single write succeeds; there are thus th ree possible
outcomes, which we list here:
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

4 C RASH CONSISTENCY : FSCK AND JOURNALING
• Just the data block (Db) is written to disk. In this case, the data is
on disk, but there is no inode that points to it and no bitmap that
even says the block is allocated. Thus, it is as if the write neve r
occurred. This case is not a problem at all, from the perspective of
ﬁle-system crash consistency 1.
• Just the updated inode (I[v2]) is written to disk. In this case, the
inode points to the disk address (5) where Db was about to be writ-
ten, but Db has not yet been written there. Thus, if we trust tha t
pointer, we will read garbage data from the disk (the old contents
of disk address 5).
Further, we have a new problem, which we call a ﬁle-system in-
consistency. The on-disk bitmap is telling us that data block 5 has
not been allocated, but the inode is saying that it has. The disag ree-
ment between the bitmap and the inode is an inconsistency in the
data structures of the ﬁle system; to use the ﬁle system, we mus t
somehow resolve this problem (more on that below).
• Just the updated bitmap (B[v2]) is written to disk. In this case, the
bitmap indicates that block 5 is allocated, but there is no inode that
points to it. Thus the ﬁle system is inconsistent again; if left unre-
solved, this write would result in a space leak , as block 5 would
never be used by the ﬁle system.
There are also three more crash scenarios in this attempt to wri te three
blocks to disk. In these cases, two writes succeed and the last one fails:
• The inode (I[v2]) and bitmap (B[v2]) are written to disk, but not
data (Db). In this case, the ﬁle system metadata is completely con-
sistent: the inode has a pointer to block 5, the bitmap indicates that
5 is in use, and thus everything looks OK from the perspective of
the ﬁle system’s metadata. But there is one problem: 5 has garbag e
in it again.
• The inode (I[v2]) and the data block (Db) are written, but not the
bitmap (B[v2]). In this case, we have the inode pointing to the cor-
rect data on disk, but again have an inconsistency between the i n-
ode and the old version of the bitmap (B1). Thus, we once again
need to resolve the problem before using the ﬁle system.
• The bitmap (B[v2]) and data block (Db) are written, but not th e
inode (I[v2]). In this case, we again have an inconsistency between
the inode and the data bitmap. However, even though the block
was written and the bitmap indicates its usage, we have no ide a
which ﬁle it belongs to, as no inode points to the ﬁle.
1However, it might be a problem for the user, who just lost some data !
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

CRASH CONSISTENCY : FSCK AND JOURNALING 5
The Crash Consistency Problem
Hopefully , from these crash scenarios, you can see the many proble ms
that can occur to our on-disk ﬁle system image because of crashes: we can
have inconsistency in ﬁle system data structures; we can have space leaks;
we can return garbage data to a user; and so forth. What we’d like to do
ideally is move the ﬁle system from one consistent state (e.g., be fore the
ﬁle got appended to) to another atomically (e.g., after the inode, bitmap,
and new data block have been written to disk). Unfortunately , w e can’t
do this easily because the disk only commits one write at a time, a nd
crashes or power loss may occur between these updates. We call thi s
general problem the crash-consistency problem (we could also call it the
consistent-update problem).
42.2 Solution #1: The File System Checker
Early ﬁle systems took a simple approach to crash consistency . Ba si-
cally , they decided to let inconsistencies happen and then ﬁx them later
(when rebooting). A classic example of this lazy approach is found in a
tool that does this: fsck2. fsck is a U NIX tool for ﬁnding such incon-
sistencies and repairing them [MK96]; similar tools to check a nd repair
a disk partition exist on different systems. Note that such an ap proach
can’t ﬁx all problems; consider, for example, the case above where the ﬁle
system looks consistent but the inode points to garbage data. The on ly
real goal is to make sure the ﬁle system metadata is internally consistent.
The tool fsck operates in a number of phases, as summarized in
McKusick and Kowalski’s paper [MK96]. It is run before the ﬁle system
is mounted and made available ( fsck assumes that no other ﬁle-system
activity is on-going while it runs); once ﬁnished, the on-disk ﬁl e system
should be consistent and thus can be made accessible to users.
Here is a basic summary of what fsck does:
• Superblock: fsck ﬁrst checks if the superblock looks reasonable,
mostly doing sanity checks such as making sure the ﬁle system si ze
is greater than the number of blocks that have been allocated. Us u-
ally the goal of these sanity checks is to ﬁnd a suspect (corrupt)
superblock; in this case, the system (or administrator) may dec ide
to use an alternate copy of the superblock.
• Free blocks: Next, fsck scans the inodes, indirect blocks, double
indirect blocks, etc., to build an understanding of which block s are
currently allocated within the ﬁle system. It uses this knowle dge
to produce a correct version of the allocation bitmaps; thus, if the re
is any inconsistency between bitmaps and inodes, it is resolved by
trusting the information within the inodes. The same type of chec k
is performed for all the inodes, making sure that all inodes that look
like they are in use are marked as such in the inode bitmaps.
2Pronounced either “eff-ess-see-kay”, “eff-ess-check”, or, if you don’t like the tool, “eff-
suck”. Yes, serious professional people use this term.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

6 C RASH CONSISTENCY : FSCK AND JOURNALING
• Inode state: Each inode is checked for corruption or other prob-
lems. For example, fsck makes sure that each allocated inode has
a valid type ﬁeld (e.g., regular ﬁle, directory , symbolic link , etc.). If
there are problems with the inode ﬁelds that are not easily ﬁxed, the
inode is considered suspect and cleared by fsck; the inode bitmap
is correspondingly updated.
• Inode links: fsck also veriﬁes the link count of each allocated in-
ode. As you may recall, the link count indicates the number of dif-
ferent directories that contain a reference (i.e., a link) to t his par-
ticular ﬁle. To verify the link count, fsck scans through the en-
tire directory tree, starting at the root directory , and builds i ts own
link counts for every ﬁle and directory in the ﬁle system. If ther e
is a mismatch between the newly-calculated count and that foun d
within an inode, corrective action must be taken, usually by ﬁxi ng
the count within the inode. If an allocated inode is discovered but
no directory refers to it, it is moved to the lost+found directory .
• Duplicates: fsck also checks for duplicate pointers, i.e., cases where
two different inodes refer to the same block. If one inode is obvi-
ously bad, it may be cleared. Alternately , the pointed-to blockcould
be copied, thus giving each inode its own copy as desired.
• Bad blocks: A check for bad block pointers is also performed while
scanning through the list of all pointers. A pointer is considered
“bad” if it obviously points to something outside its valid range,
e.g., it has an address that refers to a block greater than the p arti-
tion size. In this case, fsck can’t do anything too intelligent; it just
removes (clears) the pointer from the inode or indirect block.
• Directory checks: fsck does not understand the contents of user
ﬁles; however, directories hold speciﬁcally formatted informat ion
created by the ﬁle system itself. Thus, fsck performs additional
integrity checks on the contents of each directory , making sure t hat
“.” and “..” are the ﬁrst entries, that each inode referred to i n a
directory entry is allocated, and ensuring that no directory is linked
to more than once in the entire hierarchy .
As you can see, building a working fsck requires intricate knowledge
of the ﬁle system; making sure such a piece of code works correctly i n all
cases can be challenging [G+08]. However, fsck (and similar a pproaches)
have a bigger and perhaps more fundamental problem: they are too slow.
With a very large disk volume, scanning the entire disk to ﬁnd a ll the
allocated blocks and read the entire directory tree may take many minutes
or hours. Performance of fsck, as disks grew in capacity and RAIDs
grew in popularity , became prohibitive (despite recent advances [M+13]).
At a higher level, the basic premise of fsck seems just a tad irra-
tional. Consider our example above, where just three blocks are wr itten
to the disk; it is incredibly expensive to scan the entire dis k to ﬁx prob-
lems that occurred during an update of just three blocks. This si tuation is
akin to dropping your keys on the ﬂoor in your bedroom, and then com-
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

CRASH CONSISTENCY : FSCK AND JOURNALING 7
mencing a search-the-entire-house-for-keys recovery algorithm, starting in
the basement and working your way through every room. It works but is
wasteful. Thus, as disks (and RAIDs) grew, researchers and p ractitioners
started to look for other solutions.
42.3 Solution #2: Journaling (or Write-Ahead Logging)
Probably the most popular solution to the consistent update problem
is to steal an idea from the world of database management systems . That
idea, known as write-ahead logging, was invented to address exactly this
type of problem. In ﬁle systems, we usually call write-ahead logging jour-
naling for historical reasons. The ﬁrst ﬁle system to do this was Cedar
[H87], though many modern ﬁle systems use the idea, including L inux
ext3 and ext4, reiserfs, IBM’s JFS, SGI’s XFS, and Windows NTFS.
The basic idea is as follows. When updating the disk, before over-
writing the structures in place, ﬁrst write down a little note ( somewhere
else on the disk, in a well-known location) describing what you are about
to do. Writing this note is the “write ahead” part, and we write i t to a
structure that we organize as a “log”; hence, write-ahead loggi ng.
By writing the note to disk, you are guaranteeing that if a crash takes
places during the update (overwrite) of the structures you are u pdating,
you can go back and look at the note you made and try again; thus, you
will know exactly what to ﬁx (and how to ﬁx it) after a crash, inst ead
of having to scan the entire disk. By design, journaling thus ad ds a bit
of work during updates to greatly reduce the amount of work require d
during recovery .
We’ll now describe how Linux ext3, a popular journaling ﬁle system,
incorporates journaling into the ﬁle system. Most of the on-disk st ruc-
tures are identical to Linux ext2, e.g., the disk is divided into block groups,
and each block group contains an inode bitmap, data bitmap, inodes , and
data blocks. The new key structure is the journal itself, which occupies
some small amount of space within the partition or on another device.
Thus, an ext2 ﬁle system (without journaling) looks like this:
Super Group 0 Group 1 . . . Group N
Assuming the journal is placed within the same ﬁle system imag e
(though sometimes it is placed on a separate device, or as a ﬁle wit hin
the ﬁle system), an ext3 ﬁle system with a journal looks like this :
Super Journal Group 0 Group 1 . . . Group N
The real difference is just the presence of the journal, and of cou rse,
how it is used.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

8 C RASH CONSISTENCY : FSCK AND JOURNALING
Data Journaling
Let’s look at a simple example to understand how data journaling works.
Data journaling is available as a mode with the Linux ext3 ﬁle sy stem,
from which much of this discussion is based.
Say we have our canonical update again, where we wish to write the
inode (I[v2]), bitmap (B[v2]), and data block (Db) to disk agai n. Before
writing them to their ﬁnal disk locations, we are now ﬁrst going to write
them to the log (a.k.a. journal). This is what this will look like i n the log:
Journal
TxB I[v2] B[v2] Db TxE
You can see we have written ﬁve blocks here. The transaction begi n
(TxB) tells us about this update, including information about th e pend-
ing update to the ﬁle system (e.g., the ﬁnal addresses of the bl ocks I[v2],
B[v2], and Db), and some kind of transaction identiﬁer (TID). The mid-
dle three blocks just contain the exact contents of the blocks them selves;
this is known as physical logging as we are putting the exact physical
contents of the update in the journal (an alternate idea, logical logging ,
puts a more compact logical representation of the update in the jour nal,
e.g., “this update wishes to append data block Db to ﬁle X”, whi ch is a
little more complex but can save space in the log and perhaps impr ove
performance). The ﬁnal block (TxE) is a marker of the end of this tr ansac-
tion, and will also contain the TID.
Once this transaction is safely on disk, we are ready to overwrit e the
old structures in the ﬁle system; this process is called checkpointing.
Thus, to checkpoint the ﬁle system (i.e., bring it up to date with the pend-
ing update in the journal), we issue the writes I[v2], B[v2], a nd Db to
their disk locations as seen above; if these writes complete succ essfully ,
we have successfully checkpointed the ﬁle system and are basi cally done.
Thus, our initial sequence of operations:
1. Journal write: Write the transaction, including a transaction-begin
block, all pending data and metadata updates, and a transacti on-
end block, to the log; wait for these writes to complete.
2. Checkpoint: Write the pending metadata and data updates to their
ﬁnal locations in the ﬁle system.
In our example, we would write TxB, I[v2], B[v2], Db, and TxE to t he
journal ﬁrst. When these writes complete, we would complete the u pdate
by checkpointing I[v2], B[v2], and Db, to their ﬁnal locations on disk.
Things get a little trickier when a crash occurs during the wri tes to
the journal. Here, we are trying to write the set of blocks in the t ransac-
tion (e.g., TxB, I[v2], B[v2], Db, TxE) to disk. One simple way to do this
would be to issue each one at a time, waiting for each to complete, a nd
then issuing the next. However, this is slow. Ideally , we’d like to issue
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

CRASH CONSISTENCY : FSCK AND JOURNALING 9
ASIDE : F ORCING WRITES TO DISK
To enforce ordering between two disk writes, modern ﬁle systems have
to take a few extra precautions. In olden times, forcing ordering between
two writes, A and B, was easy: just issue the write of A to the disk, wait
for the disk to interrupt the OS when the write is complete, and t hen issue
the write of B.
Things got slightly more complex due to the increased use of write caches
within disks. With write buffering enabled (sometimes calle d immediate
reporting), a disk will inform the OS the write is complete when it simply
has been placed in the disk’s memory cache, and has not yet reache d
disk. If the OS then issues a subsequent write, it is not guaran teed to
reach the disk after previous writes; thus ordering between wr ites is not
preserved. One solution is to disable write buffering. However , more
modern systems take extra precautions and issue explicit write barriers;
such a barrier, when it completes, guarantees that all writes issued before
the barrier will reach disk before any writes issued after the barrier.
All of this machinery requires a great deal of trust in the correc t oper-
ation of the disk. Unfortunately , recent research shows that some disk
manufacturers, in an effort to deliver “higher performing” di sks, explic-
itly ignore write-barrier requests, thus making the disks se emingly run
faster but at the risk of incorrect operation [C+13, R+11]. As Kah an said,
the fast almost always beats out the slow, even if the fast is wrong .
all ﬁve block writes at once, as this would turn ﬁve writes into a s ingle
sequential write and thus be faster. However, this is unsafe, for the fol-
lowing reason: given such a big write, the disk internally may p erform
scheduling and complete small pieces of the big write in any orde r. Thus,
the disk internally may (1) write TxB, I[v2], B[v2], and TxE a nd only later
(2) write Db. Unfortunately , if the disk loses power between (1) and (2),
this is what ends up on disk:
Journal
TxB
id=1
I[v2] B[v2] ?? TxE
id=1
Why is this a problem? Well, the transaction looks like a valid tra ns-
action (it has a begin and an end with matching sequence number s). Fur-
ther, the ﬁle system can’t look at that fourth block and know it is wron g;
after all, it is arbitrary user data. Thus, if the system now re boots and
runs recovery , it will replay this transaction, and ignorantlycopy the con-
tents of the garbage block ’??’ to the location where Db is supposed t o
live. This is bad for arbitrary user data in a ﬁle; it is much wors e if it hap-
pens to a critical piece of ﬁle system, such as the superblock, w hich could
render the ﬁle system unmountable.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

10 C RASH CONSISTENCY : FSCK AND JOURNALING
ASIDE : O PTIMIZING LOG WRITES
You may have noticed a particular inefﬁciency of writing to the l og.
Namely , the ﬁle system ﬁrst has to write out the transaction-be gin block
and contents of the transaction; only after these writes complete can the
ﬁle system send the transaction-end block to disk. The performa nce im-
pact is clear, if you think about how a disk works: usually an extra rota-
tion is incurred (think about why).
One of our former graduate students, Vijayan Prabhakaran, had a simple
idea to ﬁx this problem [P+05]. When writing a transaction to th e journal,
include a checksum of the contents of the journal in the begin and e nd
blocks. Doing so enables the ﬁle system to write the entire tran saction at
once, without incurring a wait; if, during recovery , the ﬁle sys tem sees
a mismatch in the computed checksum versus the stored checksum in
the transaction, it can conclude that a crash occurred during th e write
of the transaction and thus discard the ﬁle-system update. Thu s, with a
small tweak in the write protocol and recovery system, a ﬁle syste m can
achieve faster common-case performance; on top of that, the system is
slightly more reliable, as any reads from the journal are now prote cted by
a checksum.
This simple ﬁx was attractive enough to gain the notice of Linux ﬁ le sys-
tem developers, who then incorporated it into the next generati on Linux
ﬁle system, called (you guessed it!) Linux ext4 . It now ships on mil-
lions of machines worldwide, including the Android handheld pla tform.
Thus, every time you write to disk on many Linux-based systems, a little
code developed at Wisconsin makes your system a little faster and more
reliable.
To avoid this problem, the ﬁle system issues the transactional w rite in
two steps. First, it writes all blocks except the TxE block to th e journal,
issuing these writes all at once. When these writes complete, t he journal
will look something like this (assuming our append workload again) :
Journal
TxB
id=1
I[v2] B[v2] Db
When those writes complete, the ﬁle system issues the write of th e TxE
block, thus leaving the journal in this ﬁnal, safe state:
Journal
TxB
id=1
I[v2] B[v2] Db TxE
id=1
An important aspect of this process is the atomicity guarantee pr o-
vided by the disk. It turns out that the disk guarantees that an y 512-byte
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

CRASH CONSISTENCY : FSCK AND JOURNALING 11
write will either happen or not (and never be half-written); th us, to make
sure the write of TxE is atomic, one should make it a single 512-byte block.
Thus, our current protocol to update the ﬁle system, with each of it s three
phases labeled:
1. Journal write: Write the contents of the transaction (including TxB,
metadata, and data) to the log; wait for these writes to complete .
2. Journal commit: Write the transaction commit block (containing
TxE) to the log; wait for write to complete; transaction is said to be
committed.
3. Checkpoint: Write the contents of the update (metadata and data)
to their ﬁnal on-disk locations.
Recovery
Let’s now understand how a ﬁle system can use the contents of the jour -
nal to recover from a crash. A crash may happen at any time during this
sequence of updates. If the crash happens before the transacti on is writ-
ten safely to the log (i.e., before Step 2 above completes), then our job
is easy: the pending update is simply skipped. If the crash ha ppens af-
ter the transaction has committed to the log, but before the check point is
complete, the ﬁle system can recover the update as follows. When the
system boots, the ﬁle system recovery process will scan the log and look
for transactions that have committed to the disk; these transac tions are
thus replayed (in order), with the ﬁle system again attempting to write
out the blocks in the transaction to their ﬁnal on-disk locations. T his form
of logging is one of the simplest forms there is, and is called redo logging.
By recovering the committed transactions in the journal, the ﬁle system
ensures that the on-disk structures are consistent, and thus c an proceed
by mounting the ﬁle system and readying itself for new requests .
Note that it is ﬁne for a crash to happen at any point during check-
pointing, even after some of the updates to the ﬁnal locations of the blocks
have completed. In the worst case, some of these updates are simpl y per-
formed again during recovery . Because recovery is a rare operation (only
taking place after an unexpected system crash), a few redund ant writes
are nothing to worry about 3.
Batching Log Updates
You might have noticed that the basic protocol could add a lot of extra
disk trafﬁc. For example, imagine we create two ﬁles in a row, ca lled
file1 and file2, in the same directory . To create one ﬁle, one has
to update a number of on-disk structures, minimally including : the in-
ode bitmap (to allocate a new inode), the newly-created inode of th e ﬁle,
3Unless you worry about everything, in which case we can’t help you. Stop worrying so
much, it is unhealthy! But now you’re probably worried about over-wo rrying.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

12 C RASH CONSISTENCY : FSCK AND JOURNALING
the data block of the parent directory containing the new director y en-
try , and the parent directory inode (which now has a new modiﬁcati on
time). With journaling, we logically commit all of this informati on to
the journal for each of our two ﬁle creations; because the ﬁles are i n the
same directory , and assuming they even have inodes within the s ame in-
ode block, this means that if we’re not careful, we’ll end up writin g these
same blocks over and over.
To remedy this problem, some ﬁle systems do not commit each update
to disk one at a time (e.g., Linux ext3); rather, one can buffer a ll updates
into a global transaction. In our example above, when the two ﬁles are
created, the ﬁle system just marks the in-memory inode bitmap, inodes
of the ﬁles, directory data, and directory inode as dirty , and add s them to
the list of blocks that form the current transaction. When it is ﬁn ally time
to write these blocks to disk (say , after a timeout of 5 seconds), t his single
global transaction is committed containing all of the updates des cribed
above. Thus, by buffering updates, a ﬁle system can avoid excessive write
trafﬁc to disk in many cases.
Making The Log Finite
We thus have arrived at a basic protocol for updating ﬁle-system on -disk
structures. The ﬁle system buffers updates in memory for some ti me;
when it is ﬁnally time to write to disk, the ﬁle system ﬁrst car efully writes
out the details of the transaction to the journal (a.k.a. write-a head log);
after the transaction is complete, the ﬁle system checkpoints t hose blocks
to their ﬁnal locations on disk.
However, the log is of a ﬁnite size. If we keep adding transactions to
it (as in this ﬁgure), it will soon ﬁll. What do you think happens t hen?
Journal
Tx1 Tx2 Tx3 Tx4 Tx5 ...
Two problems arise when the log becomes full. The ﬁrst is simpler ,
but less critical: the larger the log, the longer recovery will t ake, as the
recovery process must replay all the transactions within the log (in order)
to recover. The second is more of an issue: when the log is full (or nea rly
full), no further transactions can be committed to the disk, th us making
the ﬁle system “less than useful” (i.e., useless).
To address these problems, journaling ﬁle systems treat the log as a
circular data structure, re-using it over and over; this is why the journal
is sometimes referred to as a circular log. To do so, the ﬁle system must
take action some time after a checkpoint. Speciﬁcally , once a tran saction
has been checkpointed, the ﬁle system should free the space it w as occu-
pying within the journal, allowing the log space to be reused. Th ere are
many ways to achieve this end; for example, you could simply mark the
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

CRASH CONSISTENCY : FSCK AND JOURNALING 13
oldest and newest non-checkpointed transactions in the log in a journal
superblock; all other space is free. Here is a graphical depiction:
Journal
Journal
Super Tx1 Tx2 Tx3 Tx4 Tx5 ...
In the journal superblock (not to be confused with the main ﬁle sys tem
superblock), the journaling system records enough information to know
which transactions have not yet been checkpointed, and thus red uces re-
covery time as well as enables re-use of the log in a circular fash ion. And
thus we add another step to our basic protocol:
1. Journal write: Write the contents of the transaction (containing TxB
and the contents of the update) to the log; wait for these writes to
complete.
2. Journal commit: Write the transaction commit block (containing
TxE) to the log; wait for the write to complete; the transaction is
now committed.
3. Checkpoint: Write the contents of the update to their ﬁnal locations
within the ﬁle system.
4. Free: Some time later, mark the transaction free in the journal by
updating the journal superblock.
Thus we have our ﬁnal data journaling protocol. But there is still a
problem: we are writing each data block to the disk twice, which is a
heavy cost to pay , especially for something as rare as a system cr ash. Can
you ﬁgure out a way to retain consistency without writing data twi ce?
Metadata Journaling
Although recovery is now fast (scanning the journal and replayin g a few
transactions as opposed to scanning the entire disk), normal oper ation
of the ﬁle system is slower than we might desire. In particular, for each
write to disk, we are now also writing to the journal ﬁrst, thus d oubling
write trafﬁc; this doubling is especially painful during seq uential write
workloads, which now will proceed at half the peak write bandwidt h of
the drive. Further, between writes to the journal and writes t o the main
ﬁle system, there is a costly seek, which adds noticeable overhe ad for
some workloads.
Because of the high cost of writing every data block to disk twice, peo-
ple have tried a few different things in order to speed up perfor mance.
For example, the mode of journaling we described above is often call ed
data journaling (as in Linux ext3), as it journals all user data (in addition
to the metadata of the ﬁle system). A simpler (and more common) form
of journaling is sometimes called ordered journaling (or just metadata
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

14 C RASH CONSISTENCY : FSCK AND JOURNALING
journaling), and it is nearly the same, except that user data is not writ-
ten to the journal. Thus, when performing the same update as abov e, the
following information would be written to the journal:
Journal
TxB I[v2] B[v2] TxE
The data block Db, previously written to the log, would instead be
written to the ﬁle system proper, avoiding the extra write; given that most
I/O trafﬁc to the disk is data, not writing data twice substant ially reduces
the I/O load of journaling. The modiﬁcation does raise an interesti ng
question, though: when should we write data blocks to disk?
Let’s again consider our example append of a ﬁle to understand the
problem better. The update consists of three blocks: I[v2], B[v2 ], and
Db. The ﬁrst two are both metadata and will be logged and then che ck-
pointed; the latter will only be written once to the ﬁle system. W hen
should we write Db to disk? Does it matter?
As it turns out, the ordering of the data write does matter for metadata-
only journaling. For example, what if we write Db to disk after the trans-
action (containing I[v2] and B[v2]) completes? Unfortunately , this ap-
proach has a problem: the ﬁle system is consistent but I[v2] may e nd up
pointing to garbage data. Speciﬁcally , consider the case where I[v2] and
B[v2] are written but Db did not make it to disk. The ﬁle system w ill then
try to recover. Because Db is not in the log, the ﬁle system will replay
writes to I[v2] and B[v2], and produce a consistent ﬁle system ( from the
perspective of ﬁle-system metadata). However, I[v2] will be p ointing to
garbage data, i.e., at whatever was in the slot where Db was hea ded.
To ensure this situation does not arise, some ﬁle systems (e.g., L inux
ext3) write data blocks (of regular ﬁles) to the disk ﬁrst, before related
metadata is written to disk. Speciﬁcally , the protocol is as follow s:
1. Data write: Write data to ﬁnal location; wait for completion
(the wait is optional; see below for details).
2. Journal metadata write: Write the begin block and metadata to the
log; wait for writes to complete.
3. Journal commit: Write the transaction commit block (containing
TxE) to the log; wait for the write to complete; the transaction (i n-
cluding data) is now committed.
4. Checkpoint metadata: Write the contents of the metadata update
to their ﬁnal locations within the ﬁle system.
5. Free: Later, mark the transaction free in journal superblock.
By forcing the data write ﬁrst, a ﬁle system can guarantee thata pointer
will never point to garbage. Indeed, this rule of “write the poin ted-to
object before the object that points to it” is at the core of crash cons is-
tency , and is exploited even further by other crash consistency schemes
[GP94] (see below for details).
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

CRASH CONSISTENCY : FSCK AND JOURNALING 15
In most systems, metadata journaling (akin to ordered journalin g of
ext3) is more popular than full data journaling. For example, Win dows
NTFS and SGI’s XFS both use some form of metadata journaling. Linux
ext3 gives you the option of choosing either data, ordered, or unordere d
modes (in unordered mode, data can be written at any time). All of t hese
modes keep metadata consistent; they vary in their semantics f or data.
Finally , note that forcing the data write to complete (Step 1) bef ore is-
suing writes to the journal (Step 2) is not required for correctnes s, as indi-
cated in the protocol above. Speciﬁcally , it would be ﬁne to concurre ntly
issue writes to data, the transaction-begin block, and journal ed metadata;
the only real requirement is that Steps 1 and 2 complete before the issuing
of the journal commit block (Step 3).
T ricky Case: Block Reuse
There are some interesting corner cases that make journaling mor e tricky ,
and thus are worth discussing. A number of them revolve around bloc k
reuse; as Stephen Tweedie (one of the main forces behind ext3) sai d:
“What’s the hideous part of the entire system? ... It’s deletin g ﬁles.
Everything to do with delete is hairy . Everything to do with d elete...
you have nightmares around what happens if blocks get deleted a nd
then reallocated.” [T00]
The particular example Tweedie gives is as follows. Suppose you ar e
using some form of metadata journaling (and thus data blocks for ﬁle s
are not journaled). Let’s say you have a directory called foo. The user
adds an entry to foo (say by creating a ﬁle), and thus the contents of
foo (because directories are considered metadata) are written to the log;
assume the location of the foo directory data is block 1000. The log thus
contains something like this:
Journal
TxB
id=1
I[foo]
ptr:1000
D[foo]
[final addr:1000]
TxE
id=1
At this point, the user deletes everything in the directory and the di-
rectory itself, freeing up block 1000 for reuse. Finally , the us er creates a
new ﬁle (say bar), which ends up reusing the same block (1000) that used
to belong to foo. The inode of bar is committed to disk, as is its data;
note, however, because metadata journaling is in use, only the in ode of
bar is committed to the journal; the newly-written data in block 100 0 in
the ﬁle bar is not journaled.
Journal
TxB
id=1
I[foo]
ptr:1000
D[foo]
[final addr:1000]
TxE
id=1
TxB
id=2
I[bar]
ptr:1000
TxE
id=2
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

16 C RASH CONSISTENCY : FSCK AND JOURNALING
Journal File System
TxB Contents TxE Metadata Data
(metadata) (data)
issue issue issue
complete
complete
complete
issue
complete
issue issue
complete
complete
Figure 42.1: Data Journaling Timeline
Now assume a crash occurs and all of this information is still in the
log. During replay , the recovery process simply replays everything in the
log, including the write of directory data in block 1000; the repl ay thus
overwrites the user data of current ﬁle bar with old directory contents!
Clearly this is not a correct recovery action, and certainly it wi ll be a sur-
prise to the user when reading the ﬁle bar.
There are a number of solutions to this problem. One could, for ex-
ample, never reuse blocks until the delete of said blocks is chec kpointed
out of the journal. What Linux ext3 does instead is to add a new type
of record to the journal, known as a revoke record. In the case above,
deleting the directory would cause a revoke record to be written t o the
journal. When replaying the journal, the system ﬁrst scans for s uch re-
voke records; any such revoked data is never replayed, thus avoid ing the
problem mentioned above.
Wrapping Up Journaling: A Timeline
Before ending our discussion of journaling, we summarize the protoc ols
we have discussed with timelines depicting each of them. Figu re 42.1
shows the protocol when journaling data and metadata, whereas Fig ure
42.2 shows the protocol when journaling only metadata.
In each ﬁgure, time increases in the downward direction, and each row
in the ﬁgure shows the logical time that a write can be issued or mi ght
complete. For example, in the data journaling protocol (Figure 42. 1), the
writes of the transaction begin block (TxB) and the contents of the trans-
action can logically be issued at the same time, and thus can be completed
in any order; however, the write to the transaction end block (TxE ) must
not be issued until said previous writes complete. Similarly , th e check-
pointing writes to data and metadata blocks cannot begin until t he trans-
action end block has committed. Horizontal dashed lines show where
write-ordering requirements must be obeyed.
A similar timeline is shown for the metadata journaling protocol. N ote
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

CRASH CONSISTENCY : FSCK AND JOURNALING 17
Journal File System
TxB Contents TxE Metadata Data
(metadata)
issue issue issue
complete
complete
complete
issue
complete
issue
complete
Figure 42.2: Metadata Journaling Timeline
that the data write can logically be issued at the same time as t he writes
to the transaction begin and the contents of the journal; however, it must
be issued and complete before the transaction end has been issue d.
Finally , note that the time of completion marked for each write in t he
timelines is arbitrary . In a real system, completion time is de termined by
the I/O subsystem, which may reorder writes to improve performa nce.
The only guarantees about ordering that we have are those that mus t
be enforced for protocol correctness (and are shown via the horizontal
dashed lines in the ﬁgures).
42.4 Solution #3: Other Approaches
We’ve thus far described two options in keeping ﬁle system metad ata
consistent: a lazy approach based on fsck, and a more active approach
known as journaling. However, these are not the only two approaches .
One such approach, known as Soft Updates [GP94], was introduced by
Ganger and Patt. This approach carefully orders all writes to t he ﬁle sys-
tem to ensure that the on-disk structures are never left in an i nconsis-
tent state. For example, by writing a pointed-to data block to di sk before
the inode that points to it, we can ensure that the inode never poin ts to
garbage; similar rules can be derived for all the structures of the ﬁle sys-
tem. Implementing Soft Updates can be a challenge, however; whe reas
the journaling layer described above can be implemented with r elatively
little knowledge of the exact ﬁle system structures, Soft Update s requires
intricate knowledge of each ﬁle system data structure and thus adds a fair
amount of complexity to the system.
Another approach is known as copy-on-write (yes, COW), and is used
in a number of popular ﬁle systems, including Sun’s ZFS [B07]. Thi s tech-
nique never overwrites ﬁles or directories in place; rather, it places new
updates to previously unused locations on disk. After a number of u p-
dates are completed, COW ﬁle systems ﬂip the root structure of the ﬁle
system to include pointers to the newly updated structures. D oing so
makes keeping the ﬁle system consistent straightforward. We’l l be learn-
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

18 C RASH CONSISTENCY : FSCK AND JOURNALING
ing more about this technique when we discuss the log-structure d ﬁle
system (LFS) in a future chapter; LFS is an early example of a COW .
Another approach is one we just developed here at Wisconsin. In thi s
technique, entitled backpointer-based consistency (or BBC), no ordering
is enforced between writes. To achieve consistency , an additi onal back
pointer is added to every block in the system; for example, each data
block has a reference to the inode to which it belongs. When acces sing
a ﬁle, the ﬁle system can determine if the ﬁle is consistent by c hecking if
the forward pointer (e.g., the address in the inode or direct block ) points
to a block that refers back to it. If so, everything must have saf ely reached
disk and thus the ﬁle is consistent; if not, the ﬁle is inconsiste nt, and an
error is returned. By adding back pointers to the ﬁle system, a n ew form
of lazy crash consistency can be attained [C+12].
Finally , we also have explored techniques to reduce the numbe r of
times a journal protocol has to wait for disk writes to complete. Ent itled
optimistic crash consistency [C+13], this new approach issues as many
writes to disk as possible by using a generalized form of the transaction
checksum [P+05], and includes a few other techniques to detect incon-
sistencies should they arise. For some workloads, these optimisti c tech-
niques can improve performance by an order of magnitude. However, to
truly function well, a slightly different disk interface is r equired [C+13].
42.5 Summary
We have introduced the problem of crash consistency , and discuss ed
various approaches to attacking this problem. The older approach of
building a ﬁle system checker works but is likely too slow to recov er on
modern systems. Thus, many ﬁle systems now use journaling. Journ aling
reduces recovery time from O(size-of-the-disk-volume) to O(si ze-of-the-
log), thus speeding recovery substantially after a crash and r estart. For
this reason, many modern ﬁle systems use journaling. We have als o seen
that journaling can come in many different forms; the most commonly
used is ordered metadata journaling, which reduces the amount of trafﬁc
to the journal while still preserving reasonable consistency guarantees for
both ﬁle system metadata and user data. In the end, strong guara ntees
on user data are probably one of the most important things to provide;
oddly enough, as recent research has shown, this area remains a w ork in
progress [P+14].
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

CRASH CONSISTENCY : FSCK AND JOURNALING 19
References
[B07] “ZFS: The Last Word in File Systems” by Jeff Bonwick and Bill Moor e. Available online:
http://www.ostep.org/Citations/zfs_last.pdf. ZFS uses copy-on-write and journal-
ing, actually, as in some cases, logging writes to disk will perform better .
[C+12] “Consistency Without Ordering” by Vijay Chidambaram, Tushar S harma, Andrea C.
Arpaci-Dusseau, Remzi H. Arpaci-Dusseau. FAST ’12, San Jose, Cal ifornia. A recent paper of
ours about a new form of crash consistency based on back pointers. Read it for the exciting details!
[C+13] “Optimistic Crash Consistency” by Vijay Chidambaram, Thanu S. Pillai, Andrea C.
Arpaci-Dusseau, Remzi H. Arpaci-Dusseau . SOSP ’13, Nemacolin Woo dlands Resort, PA,
November 2013. Our work on a more optimistic and higher performance journaling protocol. For
workloads that call fsync() a lot, performance can be greatly improved.
[GP94] “Metadata Update Performance in File Systems” by Gregory R. G anger and Yale N.
Patt. OSDI ’94. A clever paper about using careful ordering of writes as the main way to achie ve
consistency. Implemented later in BSD-based systems.
[G+08] “SQCK: A Declarative File System Checker” by Haryadi S. Guna wi, Abhishek Ra-
jimwale, Andrea C. Arpaci-Dusseau, Remzi H. Arpaci-Dusseau. OSDI ’08, San Diego, Califor-
nia. Our own paper on a new and better way to build a ﬁle system checker using SQL queries. We also
show some problems with the existing checker, ﬁnding numerous bugs and odd behaviors, a direct result
of the complexity of fsck.
[H87] “Reimplementing the Cedar File System Using Logging and Group Commit” by Robert
Hagmann. SOSP ’87, Austin, Texas, November 1987. The ﬁrst work (that we know of) that applied
write-ahead logging (a.k.a. journaling) to a ﬁle system.
[M+13] “ffsck: The Fast File System Checker” by Ao Ma, Chris Dragga, Andre a C. Arpaci-
Dusseau, Remzi H. Arpaci-Dusseau. FAST ’13, San Jose, California , February 2013. A recent
paper of ours detailing how to make fsck an order of magnitude faster. Some of the ide as have already
been incorporated into the BSD ﬁle system checker [MK96] and are deployed tod ay.
[MK96] “Fsck – The U NIX File System Check Program” by Marshall Kirk McKusick and T. J.
Kowalski. Revised in 1996. Describes the ﬁrst comprehensive ﬁle-system checking tool, the epony-
mous fsck. Written by some of the same people who brought you FFS.
[MJLF84] “A Fast File System for UNIX” by Marshall K. McKusick, William N. Joy , Sam J.
Lefﬂer, Robert S. Fabry . ACM Transactions on Computing Systems, V olume 2:3, August 1984.
Y ou already know enough about FFS, right? But come on, it is OK to re-referenc e important papers.
[P+14] “All File Systems Are Not Created Equal: On the Complexity of Crafting Crash-Consistent
Applications” by Thanumalayan Sankaranarayana Pillai, Vijay Chidamb aram, Ramnatthan
Alagappan, Samer Al-Kiswany , Andrea C. Arpaci-Dusseau, Remzi H. A rpaci-Dusseau. OSDI
’14, Broomﬁeld, Colorado, October 2014. A paper in which we study what ﬁle systems guarantee
after crashes, and show that applications expect something different, leadi ng to all sorts of interesting
problems.
[P+05] “IRON File Systems” by Vijayan Prabhakaran, Lakshmi N. Baira vasundaram, Nitin
Agrawal, Haryadi S. Gunawi, Andrea C. Arpaci-Dusseau, Remzi H. A rpaci-Dusseau. SOSP
’05, Brighton, England, October 2005. A paper mostly focused on studying how ﬁle systems react
to disk failures. T owards the end, we introduce a transaction checksum to spe ed up logging, which was
eventually adopted into Linux ext4.
[PAA05] “Analysis and Evolution of Journaling File Systems” by Vijayan Prabhakaran, Andrea
C. Arpaci-Dusseau, Remzi H. Arpaci-Dusseau. USENIX ’05, Anaheim, California, April 2005.
An early paper we wrote analyzing how journaling ﬁle systems work.
[R+11] “Coerced Cache Eviction and Discreet-Mode Journaling” by Abhishek Rajimwale, Vijay
Chidambaram, Deepak Ramamurthi, Andrea C. Arpaci-Dusseau, Remz i H. Arpaci-Dusseau.
DSN ’11, Hong Kong, China, June 2011. Our own paper on the problem of disks that buffer writes in
a memory cache instead of forcing them to disk, even when explicitly told not to do that! Our solution
to overcome this problem: if you want A to be written to disk before B, ﬁrst write A, then send a lot of
“dummy” writes to disk, hopefully causing A to be forced to disk to make room for them in the cache. A
neat if impractical solution.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

20 C RASH CONSISTENCY : FSCK AND JOURNALING
[T98] “Journaling the Linux ext2fs File System” by Stephen C. Tweedie. The Fourth Annual
Linux Expo, May 1998. Tweedie did much of the heavy lifting in adding journaling to the Linux e xt2
ﬁle system; the result, not surprisingly, is called ext3. Some nice d esign decisions include the strong
focus on backwards compatibility, e.g., you can just add a journaling ﬁle to an e xisting ext2 ﬁle system
and then mount it as an ext3 ﬁle system.
[T00] “EXT3, Journaling Filesystem” by Stephen Tweedie. Talk at the Ot tawa Linux Sympo-
sium, July 2000. olstrans.sourceforge.net/release/OLS2000-ext 3/OLS2000-ext3.html A tran-
script of a talk given by Tweedie on ext3.
[T01] “The Linux ext2 File System” by Theodore Ts’o, June, 2001.. Avail able online here:
http://e2fsprogs.sourceforge.net/ext2.html. A simple Linux ﬁle system based on
the ideas found in FFS. For a while it was quite heavily used; now it is re ally just in the kernel as an
example of a simple ﬁle system.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

CRASH CONSISTENCY : FSCK AND JOURNALING 21
Homework (Simulation)
This section introduces fsck.py, a simple simulator you can use to
better understand how ﬁle system corruptions can be detected (a nd po-
tentially repaired). Please see the associated README for det ails on how
to run the simulator.
Questions
1. First, run fsck.py -D ; this ﬂag turns off any corruption, and thus
you can use it to generate a random ﬁle system, and see if you can
determine which ﬁles and directories are in there. So, go ahead a nd
do that! Use the -p ﬂag to see if you were right. Try this for a few
different randomly-generated ﬁle systems by setting the see d ( -s)
to different values, like 1, 2, and 3.
2. Now, let’s introduce a corruption. Run fsck.py -S 1 to start.
Can you see what inconsistency is introduced? How would you ﬁx
it in a real ﬁle system repair tool? Use -c to check if you were right.
3. Change the seed to -S 3 or -S 19 ; which inconsistency do you
see? Use -c to check your answer. What is different in these two
cases?
4. Change the seed to -S 5 ; which inconsistency do you see? How
hard would it be to ﬁx this problem in an automatic way? Use -c to
check your answer. Then, introduce a similar inconsistency with -S
38; is this harder/possible to detect? Finally , use -S 642 ; is this
inconsistency detectable? If so, how would you ﬁx the ﬁle system?
5. Change the seed to -S 6 or -S 13 ; which inconsistency do you
see? Use -c to check your answer. What is the difference across
these two cases? What should the repair tool do when encountering
such a situation?
6. Change the seed to -S 9 ; which inconsistency do you see? Use -c
to check your answer. Which piece of information should a check-
and-repair tool trust in this case?
7. Change the seed to -S 15 ; which inconsistency do you see? Use
-c to check your answer. What can a repair tool do in this case? If
no repair is possible, how much data is lost?
8. Change the seed to -S 10 ; which inconsistency do you see? Use
-c to check your answer. Is there redundancy in the ﬁle system
structure here that can help a repair?
9. Change the seed to -S 16 and -S 20 ; which inconsistency do you
see? Use -c to check your answer. How should the repair tool ﬁx
the problem?
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES
