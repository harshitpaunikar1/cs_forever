Title: file-lfs.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/file-lfs.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:36+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

43
Log-structured File Systems
In the early 90’s, a group at Berkeley led by Professor John Ousterh out
and graduate student Mendel Rosenblum developed a new ﬁle syst em
known as the log-structured ﬁle system [RO91]. Their motivation to do
so was based on the following observations:
• System memories are growing : As memory gets bigger, more data
can be cached in memory . As more data is cached, disk trafﬁc in-
creasingly consists of writes, as reads are serviced by the cac he.
Thus, ﬁle system performance is largely determined by its wri te
performance.
• There is a large gap between random I/O performance and se-
quential I/O performance : Hard-drive transfer bandwidth has in-
creased a great deal over the years [P98]; as more bits are packe d
into the surface of a drive, the bandwidth when accessing said bits
increases. Seek and rotational delay costs, however, have decrea sed
slowly; it is challenging to make cheap and small motors spin the
platters faster or move the disk arm more quickly . Thus, if you are
able to use disks in a sequential manner, you gain a sizeable pe rfor-
mance advantage over approaches that cause seeks and rotations.
• Existing ﬁle systems perform poorly on many common workloads:
For example, FFS [MJLF84] would perform a large number of writes
to create a new ﬁle of size one block: one for a new inode, one to
update the inode bitmap, one to the directory data block that the
ﬁle is in, one to the directory inode to update it, one to the new dat a
block that is a part of the new ﬁle, and one to the data bitmap to
mark the data block as allocated. Thus, although FFS places all of
these blocks within the same block group, FFS incurs many short
seeks and subsequent rotational delays and thus performance fa lls
far short of peak sequential bandwidth.
• File systems are not RAID-aware : For example, both RAID-4 and
RAID-5 have the small-write problem where a logical write to a
single block causes 4 physical I/Os to take place. Existing ﬁl e sys-
tems do not try to avoid this worst-case RAID writing behavior.
1

2 L OG-STRUCTURED FILE SYSTEMS
TIP : D ETAILS MATTER
All interesting systems are comprised of a few general ideas an d a num-
ber of details. Sometimes, when you are learning about these syste ms,
you think to yourself “Oh, I get the general idea; the rest is jus t details,”
and you use this to only half-learn how things really work. Don’t do t his!
Many times, the details are critical. As we’ll see with LFS, the general idea
is easy to understand, but to really build a working system, you have to
think through all of the tricky cases.
An ideal ﬁle system would thus focus on write performance, and try
to make use of the sequential bandwidth of the disk. Further, it would
perform well on common workloads that not only write out data but also
update on-disk metadata structures frequently . Finally , it would work
well on RAIDs as well as single disks.
The new type of ﬁle system Rosenblum and Ousterhout introduced
was called LFS, short for the Log-structured File System . When writ-
ing to disk, LFS ﬁrst buffers all updates (including metadat a!) in an in-
memory segment; when the segment is full, it is written to disk in one
long, sequential transfer to an unused part of the disk. LFS nev er over-
writes existing data, but rather always writes segments to free locations.
Because segments are large, the disk (or RAID) is used efﬁcien tly , and
performance of the ﬁle system approaches its zenith.
THE CRUX :
HOW TO MAKE ALL WRITES SEQUENTIAL WRITES ?
How can a ﬁle system transform all writes into sequential write s? For
reads, this task is impossible, as the desired block to be read m ay be any-
where on disk. For writes, however, the ﬁle system always has a ch oice,
and it is exactly this choice we hope to exploit.
43.1 Writing To Disk Sequentially
We thus have our ﬁrst challenge: how do we transform all updates t o
ﬁle-system state into a series of sequential writes to disk? T o understand
this better, let’s use a simple example. Imagine we are writin g a data block
D to a ﬁle. Writing the data block to disk might result in the follow ing
on-disk layout, with D written at disk address A0:
D
A0
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOG-STRUCTURED FILE SYSTEMS 3
However, when a user writes a data block, it is not only data that ge ts
written to disk; there is also other metadata that needs to be updated.
In this case, let’s also write the inode (I) of the ﬁle to disk, and have it
point to the data block D. When written to disk, the data block and inode
would look something like this (note that the inode looks as big as the
data block, which generally isn’t the case; in most systems, dat a blocks
are 4 KB in size, whereas an inode is much smaller, around 128 byt es):
D
A0
I
b[0]:A0
This basic idea, of simply writing all updates (such as data bl ocks,
inodes, etc.) to the disk sequentially , sits at the heart of LFS. If you un-
derstand this, you get the basic idea. But as with all complicat ed systems,
the devil is in the details.
43.2 Writing Sequentially And Effectively
Unfortunately , writing to disk sequentially is not (alone) enou gh to
guarantee efﬁcient writes. For example, imagine if we wrote a s ingle
block to address A, at time T . We then wait a little while, and write to
the disk at address A + 1 (the next block address in sequential order),
but at time T + δ. In-between the ﬁrst and second writes, unfortunately ,
the disk has rotated; when you issue the second write, it will thu s wait
for most of a rotation before being committed (speciﬁcally , if the rot ation
takes time Trotation, the disk will wait Trotation − δ before it can commit
the second write to the disk surface). And thus you can hopefully see
that simply writing to disk in sequential order is not enough to a chieve
peak performance; rather, you must issue a large number of contiguous
writes (or one large write) to the drive in order to achieve good wri te
performance.
To achieve this end, LFS uses an ancient technique known as write
buffering1. Before writing to the disk, LFS keeps track of updates in
memory; when it has received a sufﬁcient number of updates, it w rites
them to disk all at once, thus ensuring efﬁcient use of the disk.
The large chunk of updates LFS writes at one time is referred to b y
the name of a segment. Although this term is over-used in computer
systems, here it just means a large-ish chunk which LFS uses t o group
writes. Thus, when writing to disk, LFS buffers updates in an in-memory
1Indeed, it is hard to ﬁnd a good citation for this idea, since it was like ly invented by many
and very early on in the history of computing. For a study of the beneﬁt s of write buffering,
see Solworth and Orji [SO90]; to learn about its potential harms, see Mogul [M94].
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

4 L OG-STRUCTURED FILE SYSTEMS
segment, and then writes the segment all at once to the disk. As long as
the segment is large enough, these writes will be efﬁcient.
Here is an example, in which LFS buffers two sets of updates int o a
small segment; actual segments are larger (a few MB). The ﬁrs t update is
of four block writes to ﬁle j; the second is one block being added to ﬁle k.
LFS then commits the entire segment of seven blocks to disk at once . The
resulting on-disk layout of these blocks is as follows:
Dj,0
A0
Dj,1
A1
Dj,2
A2
Dj,3
A3
b[0]:A0
b[1]:A1
b[2]:A2
b[3]:A3
Inode j
Dk,0
A5
b[0]:A5
Inode k
43.3 How Much To Buffer?
This raises the following question: how many updates should LFS
buffer before writing to disk? The answer, of course, depends on t he disk
itself, speciﬁcally how high the positioning overhead is in compa rison to
the transfer rate; see the FFS chapter for a similar analysis.
For example, assume that positioning (i.e., rotation and seek over -
heads) before each write takes roughly Tposition seconds. Assume further
that the disk transfer rate is Rpeak MB/s. How much should LFS buffer
before writing when running on such a disk?
The way to think about this is that every time you write, you pay a
ﬁxed overhead of the positioning cost. Thus, how much do you have
to write in order to amortize that cost? The more you write, the better
(obviously), and the closer you get to achieving peak bandwidth.
To obtain a concrete answer, let’s assume we are writing out D MB.
The time to write out this chunk of data ( Twrite) is the positioning time
Tposition plus the time to transfer D ( D
Rpeak
), or:
Twrite = Tposition + D
Rpeak
(43.1)
And thus the effective rate of writing ( Ref f ective), which is just the
amount of data written divided by the total time to write it, is:
Ref f ective = D
Twrite
= D
Tposition + D
Rpeak
. (43.2)
What we’re interested in is getting the effective rate ( Ref f ective) close
to the peak rate. Speciﬁcally , we want the effective rate to besome fraction
F of the peak rate, where 0 < F < 1 (a typical F might be 0.9, or 90% of
the peak rate). In mathematical form, this means we want Ref f ective =
F × Rpeak.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOG-STRUCTURED FILE SYSTEMS 5
At this point, we can solve for D:
Ref f ective = D
Tposition + D
Rpeak
= F × Rpeak (43.3)
D = F × Rpeak × (Tposition + D
Rpeak
) (43.4)
D = (F × Rpeak × Tposition) + (F × Rpeak × D
Rpeak
) (43.5)
D = F
1 − F × Rpeak × Tposition (43.6)
Let’s do an example, with a disk with a positioning time of 10 mil-
liseconds and peak transfer rate of 100 MB/s; assume we want an e f-
fective bandwidth of 90% of peak ( F = 0 .9). In this case, D = 0.9
0.1 ×
100 M B/s × 0.01 seconds = 9 M B. Try some different values to see
how much we need to buffer in order to approach peak bandwidth. How
much is needed to reach 95% of peak? 99%?
43.4 Problem: Finding Inodes
To understand how we ﬁnd an inode in LFS, let us brieﬂy review how
to ﬁnd an inode in a typical U NIX ﬁle system. In a typical ﬁle system such
as FFS, or even the old U NIX ﬁle system, ﬁnding inodes is easy , because
they are organized in an array and placed on disk at ﬁxed locations .
For example, the old U NIX ﬁle system keeps all inodes at a ﬁxed por-
tion of the disk. Thus, given an inode number and the start addres s, to
ﬁnd a particular inode, you can calculate its exact disk addres s simply by
multiplying the inode number by the size of an inode, and adding t hat
to the start address of the on-disk array; array-based indexin g, given an
inode number, is fast and straightforward.
Finding an inode given an inode number in FFS is only slightly more
complicated, because FFS splits up the inode table into chunks and places
a group of inodes within each cylinder group. Thus, one must know how
big each chunk of inodes is and the start addresses of each. After that, the
calculations are similar and also easy .
In LFS, life is more difﬁcult. Why? Well, we’ve managed to scatte r the
inodes all throughout the disk! Worse, we never overwrite in place , and
thus the latest version of an inode (i.e., the one we want) keeps mov ing.
43.5 Solution Through Indirection: The Inode Map
To remedy this, the designers of LFS introduced a level of indirection
between inode numbers and the inodes through a data structure ca lled
the inode map (imap). The imap is a structure that takes an inode number
as input and produces the disk address of the most recent version of the
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

6 L OG-STRUCTURED FILE SYSTEMS
TIP : U SE A L EVEL OF INDIRECTION
People often say that the solution to all problems in Computer Scienc e is
simply a level of indirection. This is clearly not true; it is just the solution
to most problems (yes, this is still too strong of a comment, but you get the
point). You certainly can think of every virtualization we have s tudied,
e.g., virtual memory , or the notion of a ﬁle, as simply a level of indirection.
And certainly the inode map in LFS is a virtualization of inode num bers.
Hopefully you can see the great power of indirection in these examp les,
allowing us to freely move structures around (such as pages in th e VM
example, or inodes in LFS) without having to change every referen ce to
them. Of course, indirection can have a downside too: extra overhead. So
next time you have a problem, try solving it with indirection, but make
sure to think about the overheads of doing so ﬁrst. As Wheeler famou sly
said, “All problems in computer science can be solved by another l evel of
indirection, except of course for the problem of too many indirection s.”
inode. Thus, you can imagine it would often be implemented as a sim ple
array, with 4 bytes (a disk pointer) per entry . Any time an inode is written
to disk, the imap is updated with its new location.
The imap, unfortunately , needs to be kept persistent (i.e., w ritten to
disk); doing so allows LFS to keep track of the locations of inodes acr oss
crashes, and thus operate as desired. Thus, a question: where s hould the
imap reside on disk?
It could live on a ﬁxed part of the disk, of course. Unfortunately , as it
gets updated frequently , this would then require updates to ﬁle structures
to be followed by writes to the imap, and hence performance would suffer
(i.e., there would be more disk seeks, between each update and t he ﬁxed
location of the imap).
Instead, LFS places chunks of the inode map right next to where i t is
writing all of the other new information. Thus, when appending a d ata
block to a ﬁle k, LFS actually writes the new data block, its inode, and a
piece of the inode map all together onto the disk, as follows:
D
A0
I[k]
b[0]:A0
A1
imap
m[k]:A1
In this picture, the piece of the imap array stored in the block ma rked
imap tells LFS that the inode k is at disk address A1; this inode, in turn,
tells LFS that its data block D is at address A0.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOG-STRUCTURED FILE SYSTEMS 7
43.6 Completing The Solution: The Checkpoint Region
The clever reader (that’s you, right?) might have noticed a probl em
here. How do we ﬁnd the inode map, now that pieces of it are also now
spread across the disk? In the end, there is no magic: the ﬁle sy stem must
have some ﬁxed and known location on disk to begin a ﬁle lookup.
LFS has just such a ﬁxed place on disk for this, known as the check-
point region (CR) . The checkpoint region contains pointers to (i.e., ad-
dresses of) the latest pieces of the inode map, and thus the inode m ap
pieces can be found by reading the CR ﬁrst. Note the checkpoint re gion
is only updated periodically (say every 30 seconds or so), and thus perfor-
mance is not ill-affected. Thus, the overall structure of the on- disk layout
contains a checkpoint region (which points to the latest pieces of the in-
ode map); the inode map pieces each contain addresses of the inodes ; the
inodes point to ﬁles (and directories) just like typical U NIX ﬁle systems.
Here is an example of the checkpoint region (note it is all the way a t
the beginning of the disk, at address 0), and a single imap chun k, inode,
and data block. A real ﬁle system would of course have a much bigger
CR (indeed, it would have two, as we’ll come to understand later), many
imap chunks, and of course many more inodes, data blocks, etc.
imap
[k...k+N]:
A2
CR
0
D
A0
I[k]
b[0]:A0
A1
imap
m[k]:A1
A2
43.7 Reading A File From Disk: A Recap
To make sure you understand how LFS works, let us now walk through
what must happen to read a ﬁle from disk. Assume we have nothing i n
memory to begin. The ﬁrst on-disk data structure we must read is the
checkpoint region. The checkpoint region contains pointers (i.e. , disk ad-
dresses) to the entire inode map, and thus LFS then reads in the entire in-
ode map and caches it in memory . After this point, when given an in ode
number of a ﬁle, LFS simply looks up the inode-number to inode-disk -
address mapping in the imap, and reads in the most recent versi on of the
inode. To read a block from the ﬁle, at this point, LFS proceeds exac tly
as a typical U NIX ﬁle system, by using direct pointers or indirect pointers
or doubly-indirect pointers as need be. In the common case, LFS shou ld
perform the same number of I/Os as a typical ﬁle system when read ing a
ﬁle from disk; the entire imap is cached and thus the extra work L FS does
during a read is to look up the inode’s address in the imap.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

8 L OG-STRUCTURED FILE SYSTEMS
43.8 What About Directories?
Thus far, we’ve simpliﬁed our discussion a bit by only considering in-
odes and data blocks. However, to access a ﬁle in a ﬁle system (suc h as
/home/remzi/foo, one of our favorite fake ﬁle names), some directo-
ries must be accessed too. So how does LFS store directory data?
Fortunately , directory structure is basically identical to c lassic U NIX
ﬁle systems, in that a directory is just a collection of (name, inode number)
mappings. For example, when creating a ﬁle on disk, LFS must both write
a new inode, some data, as well as the directory data and its inode t hat
refer to this ﬁle. Remember that LFS will do so sequentially on the disk
(after buffering the updates for some time). Thus, creating a ﬁ le foo in a
directory would lead to the following new structures on disk:
Dk
A0
I[k]
b[0]:A0
A1
(foo, k)
Ddir
A2
I[dir]
b[0]:A2
A3
m[k]:A1
m[dir]:A3
imap
The piece of the inode map contains the information for the location of
both the directory ﬁle dir as well as the newly-created ﬁle f . Thus, when
accessing ﬁle foo (with inode number k), you would ﬁrst look in the
inode map (usually cached in memory) to ﬁnd the location of the inode
of directory dir (A3); you then read the directory inode, which gives you
the location of the directory data ( A2); reading this data block gives you
the name-to-inode-number mapping of ( foo, k). You then consult the
inode map again to ﬁnd the location of inode number k (A1), and ﬁnally
read the desired data block at address A0.
There is one other serious problem in LFS that the inode map solves,
known as the recursive update problem [Z+12]. The problem arises
in any ﬁle system that never updates in place (such as LFS), but rather
moves updates to new locations on the disk.
Speciﬁcally , whenever an inode is updated, its location on disk changes.
If we hadn’t been careful, this would have also entailed an upda te to
the directory that points to this ﬁle, which then would have mand ated
a change to the parent of that directory , and so on, all the way up t he ﬁle
system tree.
LFS cleverly avoids this problem with the inode map. Even though
the location of an inode may change, the change is never reﬂected i n the
directory itself; rather, the imap structure is updated whil e the directory
holds the same name-to-inode-number mapping. Thus, through ind irec-
tion, LFS avoids the recursive update problem.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOG-STRUCTURED FILE SYSTEMS 9
43.9 A New Problem: Garbage Collection
You may have noticed another problem with LFS; it repeatedly write s
the latest version of a ﬁle (including its inode and data) to new l ocations
on disk. This process, while keeping writes efﬁcient, implies that LFS
leaves old versions of ﬁle structures scattered throughout the di sk. We
(rather unceremoniously) call these old versions garbage.
For example, let’s imagine the case where we have an existing ﬁl e re-
ferred to by inode number k, which points to a single data block D0.
We now update that block, generating both a new inode and a new data
block. The resulting on-disk layout of LFS would look something like t his
(note we omit the imap and other structures for simplicity; a new c hunk
of imap would also have to be written to disk to point to the new inod e):
D0
A0
I[k]
b[0]:A0
(garbage)
D0
A4
I[k]
b[0]:A4
In the diagram, you can see that both the inode and data block have
two versions on disk, one old (the one on the left) and one current and
thus live (the one on the right). By the simple act of (logically) updating
a data block, a number of new structures must be persisted by LFS, thus
leaving old versions of said blocks on the disk.
As another example, imagine we instead append a block to that ori g-
inal ﬁle k. In this case, a new version of the inode is generated, but the
old data block is still pointed to by the inode. Thus, it is still li ve and very
much part of the current ﬁle system:
D0
A0
I[k]
b[0]:A0
(garbage)
D1
A4
b[0]:A0
b[1]:A4
I[k]
So what should we do with these older versions of inodes, data blocks,
and so forth? One could keep those older versions around and allow
users to restore old ﬁle versions (for example, when they acciden tally
overwrite or delete a ﬁle, it could be quite handy to do so); such a ﬁ le
system is known as a versioning ﬁle system because it keeps track of the
different versions of a ﬁle.
However, LFS instead keeps only the latest live version of a ﬁle; t hus
(in the background), LFS must periodically ﬁnd these old dead ve rsions
of ﬁle data, inodes, and other structures, and clean them; cleaning should
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

10 L OG-STRUCTURED FILE SYSTEMS
thus make blocks on disk free again for use in subsequent writes. Note
that the process of cleaning is a form of garbage collection , a technique
that arises in programming languages that automatically freeunused mem-
ory for programs.
Earlier we discussed segments as important as they are the mechanism
that enables large writes to disk in LFS. As it turns out, they ar e also quite
integral to effective cleaning. Imagine what would happen if the LFS
cleaner simply went through and freed single data blocks, inode s, etc.,
during cleaning. The result: a ﬁle system with some number of fr ee holes
mixed between allocated space on disk. Write performance would d rop
considerably , as LFS would not be able to ﬁnd a large contiguous reg ion
to write to disk sequentially and with high performance.
Instead, the LFS cleaner works on a segment-by-segment basis, thus
clearing up large chunks of space for subsequent writing. The basic clean-
ing process works as follows. Periodically , the LFS cleaner reads in a
number of old (partially-used) segments, determines which bl ocks are
live within these segments, and then write out a new set of segme nts
with just the live blocks within them, freeing up the old ones for w riting.
Speciﬁcally , we expect the cleaner to read in M existing segments, com-
pact their contents into N new segments (where N < M ), and then write
the N segments to disk in new locations. The old M segments are then
freed and can be used by the ﬁle system for subsequent writes.
We are now left with two problems, however. The ﬁrst is mechanism :
how can LFS tell which blocks within a segment are live, and whic h are
dead? The second is policy: how often should the cleaner run, and wh ich
segments should it pick to clean?
43.10 Determining Block Liveness
We address the mechanism ﬁrst. Given a data block D within an on-
disk segment S, LFS must be able to determine whether D is live. To do
so, LFS adds a little extra information to each segment that desc ribes each
block. Speciﬁcally , LFS includes, for each data block D, its inode number
(which ﬁle it belongs to) and its offset (which block of the ﬁle this is). This
information is recorded in a structure at the head of the segment k nown
as the segment summary block .
Given this information, it is straightforward to determine whe ther a
block is live or dead. For a block D located on disk at address A, look
in the segment summary block and ﬁnd its inode number N and offset
T . Next, look in the imap to ﬁnd where N lives and read N from disk
(perhaps it is already in memory , which is even better). Final ly , using
the offset T , look in the inode (or some indirect block) to see where the
inode thinks the Tth block of this ﬁle is on disk. If it points exactl y to disk
address A, LFS can conclude that the block D is live. If it points anywhere
else, LFS can conclude that D is not in use (i.e., it is dead) and thus know
that this version is no longer needed. Here is a pseudocode summar y:
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOG-STRUCTURED FILE SYSTEMS 11
(N, T) = SegmentSummary[A];
inode = Read(imap[N]);
if (inode[T] == A)
// block D is alive
else
// block D is garbage
Here is a diagram depicting the mechanism, in which the segme nt
summary block (marked SS ) records that the data block at address A0
is actually a part of ﬁle k at offset 0. By checking the imap for k, you can
ﬁnd the inode, and see that it does indeed point to that location.
D
A0
I[k]
b[0]:A0
A1
imap
m[k]:A1A0:
(k,0)
ss
There are some shortcuts LFS takes to make the process of determining
liveness more efﬁcient. For example, when a ﬁle is truncated or d eleted,
LFS increases its version number and records the new version number in
the imap. By also recording the version number in the on-disk seg ment,
LFS can short circuit the longer check described above simply by compar-
ing the on-disk version number with a version number in the imap, thus
avoiding extra reads.
43.11 A Policy Question: Which Blocks To Clean, And When?
On top of the mechanism described above, LFS must include a set of
policies to determine both when to clean and which blocks are wort h
cleaning. Determining when to clean is easier; either period ically , dur-
ing idle time, or when you have to because the disk is full.
Determining which blocks to clean is more challenging, and has been
the subject of many research papers. In the original LFS paper [ RO91], the
authors describe an approach which tries to segregate hot and cold seg-
ments. A hot segment is one in which the contents are being freque ntly
over-written; thus, for such a segment, the best policy is to wai t a long
time before cleaning it, as more and more blocks are getting over-w ritten
(in new segments) and thus being freed for use. A cold segment, i n con-
trast, may have a few dead blocks but the rest of its contents are r elatively
stable. Thus, the authors conclude that one should clean cold segm ents
sooner and hot segments later, and develop a heuristic that does ex actly
that. However, as with most policies, this policy isn’t perfect; l ater ap-
proaches show how to do better [MR+97].
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

12 L OG-STRUCTURED FILE SYSTEMS
43.12 Crash Recovery And The Log
One ﬁnal problem: what happens if the system crashes while LFS is
writing to disk? As you may recall in the previous chapter about j our-
naling, crashes during updates are tricky for ﬁle systems, an d thus some-
thing LFS must consider as well.
During normal operation, LFS buffers writes in a segment, and th en
(when the segment is full, or when some amount of time has elapsed) ,
writes the segment to disk. LFS organizes these writes in a log, i.e., the
checkpoint region points to a head and tail segment, and each seg ment
points to the next segment to be written. LFS also periodically updates the
checkpoint region. Crashes could clearly happen during either of these
operations (write to a segment, write to the CR). So how does LFS han dle
crashes during writes to these structures?
Let’s cover the second case ﬁrst. To ensure that the CR update hap pens
atomically , LFS actually keeps two CRs, one at either end of the d isk, and
writes to them alternately . LFS also implements a careful pr otocol when
updating the CR with the latest pointers to the inode map and other infor-
mation; speciﬁcally , it ﬁrst writes out a header (with timestamp), then the
body of the CR, and then ﬁnally one last block (also with a timestam p). If
the system crashes during a CR update, LFS can detect this by s eeing an
inconsistent pair of timestamps. LFS will always choose to use th e most
recent CR that has consistent timestamps, and thus consistent update of
the CR is achieved.
Let’s now address the ﬁrst case. Because LFS writes the CR every 30
seconds or so, the last consistent snapshot of the ﬁle system may be q uite
old. Thus, upon reboot, LFS can easily recover by simply reading in the
checkpoint region, the imap pieces it points to, and subsequent ﬁ les and
directories; however, the last many seconds of updates would be los t.
To improve upon this, LFS tries to rebuild many of those segments
through a technique known as roll forward in the database community .
The basic idea is to start with the last checkpoint region, ﬁnd t he end of
the log (which is included in the CR), and then use that to read t hrough
the next segments and see if there are any valid updates withi n it. If there
are, LFS updates the ﬁle system accordingly and thus recovers m uch of
the data and metadata written since the last checkpoint. See Ros enblum’s
award-winning dissertation for details [R92].
43.13 Summary
LFS introduces a new approach to updating the disk. Instead of ove r-
writing ﬁles in places, LFS always writes to an unused portion of the
disk, and then later reclaims that old space through cleaning. This ap-
proach, which in database systems is called shadow paging [L77] and in
ﬁle-system-speak is sometimes called copy-on-write, enables highly efﬁ-
cient writing, as LFS can gather all updates into an in-memory segment
and then write them out together sequentially .
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOG-STRUCTURED FILE SYSTEMS 13
TIP : T URN FLAWS INTO VIRTUES
Whenever your system has a fundamental ﬂaw, see if you can turn i t
around into a feature or something useful. NetApp’s WAFL does this
with old ﬁle contents; by making old versions available, WAFL no l onger
has to worry about cleaning quite so often (though it does delete old ver-
sions, eventually , in the background), and thus provides a cool fe ature
and removes much of the LFS cleaning problem all in one wonderful
twist. Are there other examples of this in systems? Undoubtedly , but
you’ll have to think of them yourself, because this chapter is over with a
capital “O”. Over. Done. Kaput. We’re out. Peace!
The large writes that LFS generates are excellent for performa nce on
many different devices. On hard drives, large writes ensure that posi-
tioning time is minimized; on parity-based RAIDs, such as RAID -4 and
RAID-5, they avoid the small-write problem entirely . Recent research has
even shown that large I/Os are required for high performance on Fl ash-
based SSDs [HK+17]; thus, perhaps surprisingly , LFS-style ﬁle systems
may be an excellent choice even for these new mediums.
The downside to this approach is that it generates garbage; old c opies
of the data are scattered throughout the disk, and if one wants to r e-
claim such space for subsequent usage, one must clean old segmen ts pe-
riodically . Cleaning became the focus of much controversy in LFS, a nd
concerns over cleaning costs [SS+95] perhaps limited LFS’s initial impact
on the ﬁeld. However, some modern commercial ﬁle systems, includi ng
NetApp’s WAFL [HLM94], Sun’s ZFS [B07], and Linux btrfs [R+13], and
even modern ﬂash-based SSDs [AD14], adopt a similar copy-on-write
approach to writing to disk, and thus the intellectual legacy of LFS lives
on in these modern ﬁle systems. In particular, WAFL got around cle an-
ing problems by turning them into a feature; by providing old ver sions of
the ﬁle system via snapshots, users could access old ﬁles whenever they
deleted current ones accidentally .
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

14 L OG-STRUCTURED FILE SYSTEMS
References
[AD14] “Operating Systems: Three Easy Pieces” (Chapter: Flash-based So lid State Drives)
by Remzi Arpaci-Dusseau and Andrea Arpaci-Dusseau. Arpaci-Dusseau Books, 2014. A bit
gauche to refer you to another chapter in this very book, but who are we to judge?
[B07] “ZFS: The Last Word in File Systems” by Jeff Bonwick and Bill Moor e. Copy Available:
http://www.ostep.org/Citations/zfs_last.pdf. Slides on ZFS; unfortunately, there
is no great ZFS paper (yet). Maybe you will write one, so we can cite it here?
[HK+17] “The Unwritten Contract of of Solid State Drives” by Jun He, S udarsun Kannan, An-
drea C. Arpaci-Dusseau, Remzi H. Arpaci-Dusseau. EuroSys ’17, A pril 2017. Which unwritten
rules one must follow to extract high performance from an SSD? Interestingl y, both request scale (large
or parallel requests) and locality still matter, even on SSDs. The more things change ...
[HLM94] “File System Design for an NFS File Server Appliance” by Da ve Hitz, James Lau,
Michael Malcolm. USENIX Spring ’94. WAFL takes many ideas from LFS and RAID and puts it
into a high-speed NFS appliance for the multi-billion dollar storage company N etApp.
[L77] “Physical Integrity in a Large Segmented Database” by R. Lori e. ACM Transactions on
Databases, V olume 2:1, 1977. The original idea of shadow paging is presented here.
[MJLF84] “A Fast File System for UNIX” by Marshall K. McKusick, William N. Joy , Sam J.
Lefﬂer, Robert S. Fabry . ACM TOCS, V olume 2:3, August 1984. The original FFS paper; see the
chapter on FFS for more details.
[MR+97] “Improving the Performance of Log-structured File Systems wit h Adaptive Meth-
ods” by Jeanna Neefe Matthews, Drew Roselli, Adam M. Costello, Randol ph Y . Wang, Thomas
E. Anderson. SOSP 1997, pages 238-251, October, Saint Malo, France. A more recent paper detail-
ing better policies for cleaning in LFS.
[M94] “A Better Update Policy” by Jeffrey C. Mogul. USENIX ATC ’94, June 1 994. In this paper,
Mogul ﬁnds that read workloads can be harmed by buffering writes for too long and then sending them
to the disk in a big burst. Thus, he recommends sending writes more fr equently and in smaller batches.
[P98] “Hardware Technology Trends and Database Opportunities” by Dav id A. Patterson.
ACM SIGMOD ’98 Keynote, 1998. Available online here: http://www.cs.berkeley.edu/
˜pattrsn/talks/keynote.html. A great set of slides on technology trends in computer sys-
tems. Hopefully, Patterson will create another of these sometime soon.
[R+13] “BTRFS: The Linux B-Tree Filesystem” by Ohad Rodeh, Josef Bacik, Chris Mason. ACM
Transactions on Storage, V olume 9 Issue 3, August 2013. Finally, a good paper on BTRFS, a
modern take on copy-on-write ﬁle systems.
[RO91] “Design and Implementation of the Log-structured File Syste m” by Mendel Rosen-
blum and John Ousterhout. SOSP ’91, Paciﬁc Grove, CA, October 1991. The original SOSP
paper about LFS, which has been cited by hundreds of other papers and insp ired many real systems.
[R92] “Design and Implementation of the Log-structured File Syste m” by Mendel Rosenblum.
http://www.eecs.berkeley .edu/Pubs/TechRpts/1992/CSD-92-696.pdf. The award-winning dis-
sertation about LFS, with many of the details missing from the paper.
[SS+95] “File system logging versus clustering: a performance compa rison” by Margo Seltzer,
Keith A. Smith, Hari Balakrishnan, Jacqueline Chang, Sara McMains, V enkata Padmanabhan.
USENIX 1995 Technical Conference, New Orleans, Louisiana, 1995. A paper that showed the LFS
performance sometimes has problems, particularly for workloads with many call s to fsync() (such as
database workloads). The paper was controversial at the time.
[SO90] “Write-Only Disk Caches” by Jon A. Solworth, Cyril U. Orji. SIGMOD ’ 90, Atlantic
City , New Jersey , May 1990. An early study of write buffering and its beneﬁts. However, buffering
for too long can be harmful: see Mogul [M94] for details.
[Z+12] “De-indirection for Flash-based SSDs with Nameless Writes” by Yiying Zhang, Leo
Prasath Arulraj, Andrea C. Arpaci-Dusseau, Remzi H. Arpaci-Dusse au. FAST ’13, San Jose,
California, February 2013. Our paper on a new way to build ﬂash-based storage devices, to avoid
redundant mappings in the ﬁle system and FTL. The idea is for the devic e to pick the physical location
of a write, and return the address to the ﬁle system, which stores the mapping .
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOG-STRUCTURED FILE SYSTEMS 15
Homework (Simulation)
This section introduces lfs.py, a simple LFS simulator you can use
to understand better how an LFS-based ﬁle system works. Read the
README for details on how to run the simulator.
Questions
1. Run ./lfs.py -n 3 , perhaps varying the seed ( -s). Can you ﬁg-
ure out which commands were run to generate the ﬁnal ﬁle system
contents? Can you tell which order those commands were issued?
Finally , can you determine the liveness of each block in the ﬁnal
ﬁle system state? Use -o to show which commands were run, and
-c to show the liveness of the ﬁnal ﬁle system state. How much
harder does the task become for you as you increase the number of
commands issued (i.e., change -n 3 to -n 5 )?
2. If you ﬁnd the above painful, you can help yourself a little bit b y
showing the set of updates caused by each speciﬁc command. To do
so, run ./lfs.py -n 3 -i . Now see if it is easier to understand
what each command must have been. Change the random seed to
get different commands to interpret (e.g., -s 1 , -s 2 , -s 3 , etc.).
3. To further test your ability to ﬁgure out what updates are mad e to
disk by each command, run the following: ./lfs.py -o -F -s
100 (and perhaps a few other random seeds). This just shows a
set of commands and does NOT show you the ﬁnal state of the ﬁle
system. Can you reason about what the ﬁnal state of the ﬁle system
must be?
4. Now see if you can determine which ﬁles and directories are liv e
after a number of ﬁle and directory operations. Run tt ./lfs.py
-n 20 -s 1 and then examine the ﬁnal ﬁle system state. Can you
ﬁgure out which pathnames are valid? Run tt ./lfs.py -n 20
-s 1 -c -v to see the results. Run with -o to see if your answers
match up given the series of random commands. Use different ran-
dom seeds to get more problems.
5. Now let’s issue some speciﬁc commands. First, let’s create a ﬁle
and write to it repeatedly . To do so, use the -L ﬂag, which lets you
specify speciﬁc commands to execute. Let’s create the ﬁle ”/foo”
and write to it four times:
-L c,/foo:w,/foo,0,1:w,/foo,1,1:w,/foo,2,1:w,/foo,3, 1
-o. See if you can determine the liveness of the ﬁnal ﬁle system
state; use -c to check your answers.
6. Now, let’s do the same thing, but with a single write operation i n-
stead of four. Run ./lfs.py -o -L c,/foo:w,/foo,0,4 to
create ﬁle ”/foo” and write 4 blocks with a single write operation.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

16 L OG-STRUCTURED FILE SYSTEMS
Compute the liveness again, and check if you are right with -c.
What is the main difference between writing a ﬁle all at once (a s
we do here) versus doing it one block at a time (as above)? What
does this tell you about the importance of buffering updates in main
memory as the real LFS does?
7. Let’s do another speciﬁc example. First, run the following: ./lfs.py
-L c,/foo:w,/foo,0,1 . What does this set of commands do?
Now, run ./lfs.py -L c,/foo:w,/foo,7,1 . What does this
set of commands do? How are the two different? What can you tell
about the size ﬁeld in the inode from these two sets of commands?
8. Now let’s look explicitly at ﬁle creation versus directory creat ion.
Run simulations ./lfs.py -L c,/foo and ./lfs.py -L d,/foo
to create a ﬁle and then a directory . What is similar about theseruns,
and what is different?
9. The LFS simulator supports hard links as well. Run the followin g
to study how they work:
./lfs.py -L c,/foo:l,/foo,/bar:l,/foo,/goo -o -i .
What blocks are written out when a hard link is created? How is
this similar to just creating a new ﬁle, and how is it different ? How
does the reference count ﬁeld change as links are created?
10. LFS makes many different policy decisions. We do not explore
many of them here – perhaps something left for the future – but here
is a simple one we do explore: the choice of inode number. First, run
./lfs.py -p c100 -n 10 -o -a s to show the usual behav-
ior with the ”sequential” allocation policy , which tries to use f ree
inode numbers nearest to zero. Then, change to a ”random” policy
by running ./lfs.py -p c100 -n 10 -o -a r (the -p c100
ﬂag ensures 100 percent of the random operations are ﬁle creations).
What on-disk differences does a random policy versus a sequentia l
policy result in? What does this say about the importance of choos-
ing inode numbers in a real LFS?
11. One last thing we’ve been assuming is that the LFS simulator al-
ways updates the checkpoint region after each update. In the re al
LFS, that isn’t the case: it is updated periodically to avoid long
seeks. Run ./lfs.py -N -i -o -s 1000 to see some opera-
tions and the intermediate and ﬁnal states of the ﬁle system whe n
the checkpoint region isn’t forced to disk. What would happen if
the checkpoint region is never updated? What if it is updated pe ri-
odically? Could you ﬁgure out how to recover the ﬁle system to the
latest state by rolling forward in the log?
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
