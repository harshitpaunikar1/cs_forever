Title: file-ffs.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/file-ffs.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:23+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

41
Locality and The Fast File System
When the U NIX operating system was ﬁrst introduced, the U NIX wiz-
ard himself Ken Thompson wrote the ﬁrst ﬁle system. Let’s call tha t the
“old U NIX ﬁle system”, and it was really simple. Basically , its data st ruc-
tures looked like this on the disk:
S Inodes Data
The super block (S) contained information about the entire ﬁle syst em:
how big the volume is, how many inodes there are, a pointer to the hea d
of a free list of blocks, and so forth. The inode region of the disk conta ined
all the inodes for the ﬁle system. Finally , most of the disk was tak en up
by data blocks.
The good thing about the old ﬁle system was that it was simple, and
supported the basic abstractions the ﬁle system was trying to d eliver: ﬁles
and the directory hierarchy . This easy-to-use system was a rea l step for-
ward from the clumsy , record-based storage systems of the past, a nd the
directory hierarchy was a true advance over simpler, one-levelhierarchies
provided by earlier systems.
41.1 The Problem: Poor Performance
The problem: performance was terrible. As measured by Kirk McK u-
sick and his colleagues at Berkeley [MJLF84], performance sta rted off bad
and got worse over time, to the point where the ﬁle system was deliv ering
only 2% of overall disk bandwidth!
The main issue was that the old UNIX ﬁle system treated the disk like it
was a random-access memory; data was spread all over the place wi thout
regard to the fact that the medium holding the data was a disk, a nd thus
had real and expensive positioning costs. For example, the data b locks of
a ﬁle were often very far away from its inode, thus inducing an exp ensive
seek whenever one ﬁrst read the inode and then the data blocks of a ﬁ le
(a pretty common operation).
1

2 L OCALITY AND THE FAST FILE SYSTEM
Worse, the ﬁle system would end up getting quite fragmented, as the
free space was not carefully managed. The free list would end up point-
ing to a bunch of blocks spread across the disk, and as ﬁles got alloc ated,
they would simply take the next free block. The result was that a logi-
cally contiguous ﬁle would be accessed by going back and forth acros s
the disk, thus reducing performance dramatically .
For example, imagine the following data block region, which contai ns
four ﬁles (A, B, C, and D), each of size 2 blocks:
A1 A2 B1 B2 C1 C2 D1 D2
If B and D are deleted, the resulting layout is:
A1 A2 C1 C2
As you can see, the free space is fragmented into two chunks of tw o
blocks, instead of one nice contiguous chunk of four. Let’s say you now
wish to allocate a ﬁle E, of size four blocks:
A1 A2 E1 E2 C1 C2 E3 E4
You can see what happens: E gets spread across the disk, and as a
result, when accessing E, you don’t get peak (sequential) perfor mance
from the disk. Rather, you ﬁrst read E1 and E2, then seek, then re ad E3
and E4. This fragmentation problem happened all the time in the old
UNIX ﬁle system, and it hurt performance. A side note: this problem is
exactly what disk defragmentation tools help with; they reorganize on-
disk data to place ﬁles contiguously and make free space for one or a few
contiguous regions, moving data around and then rewriting inodes a nd
such to reﬂect the changes.
One other problem: the original block size was too small (512 bytes ).
Thus, transferring data from the disk was inherently inefﬁci ent. Smaller
blocks were good because they minimized internal fragmentation (waste
within the block), but bad for transfer as each block might requi re a posi-
tioning overhead to reach it. Thus, the problem:
THE CRUX :
HOW TO ORGANIZE ON-DISK DATA TO IMPROVE PERFORMANCE
How can we organize ﬁle system data structures so as to improve pe r-
formance? What types of allocation policies do we need on top of those
data structures? How do we make the ﬁle system “disk aware”?
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOCALITY AND THE FAST FILE SYSTEM 3
41.2 FFS: Disk Awareness Is The Solution
A group at Berkeley decided to build a better, faster ﬁle syste m, which
they cleverly called the Fast File System (FFS) . The idea was to design
the ﬁle system structures and allocation policies to be “disk aw are” and
thus improve performance, which is exactly what they did. FFS t hus ush-
ered in a new era of ﬁle system research; by keeping the same interface
to the ﬁle system (the same APIs, including open(), read(), write(),
close(), and other ﬁle system calls) but changing the internal implemen-
tation, the authors paved the path for new ﬁle system construction, work
that continues today . Virtually all modern ﬁle systems adhere t o the ex-
isting interface (and thus preserve compatibility with appl ications) while
changing their internals for performance, reliability , or other reasons.
41.3 Organizing Structure: The Cylinder Group
The ﬁrst step was to change the on-disk structures. FFS divide s the
disk into a number of cylinder groups. A single cylinder is a set of tracks
on different surfaces of a hard drive that are the same distance from the
center of the drive; it is called a cylinder because of its clear resemblance
to the so-called geometrical shape. FFS aggregates N consecutive cylin-
ders into a group, and thus the entire disk can thus be viewed as a collec-
tion of cylinder groups. Here is a simple example, showing the four outer
most tracks of a drive with six platters, and a cylinder group tha t consists
of three cylinders:
Single track (e.g., dark gray)
Cylinder:
Tracks at same distance from center
of drive across different surfaces
[all tracks with same color]
Cylinder Group:
Set of N consecutive cylinders
[if N=3, first group does
not include black track]
Note that modern drives do not export enough information for the
ﬁle system to truly understand whether a particular cylinde r is in use;
as discussed previously [AD18a], disks export a logical addres s space of
blocks and hide details of their geometry from clients. Thus, mode rn ﬁle
© 2008–26, A RPACI -D USSEAU THREE
EASY
PIECES

4 L OCALITY AND THE FAST FILE SYSTEM
systems (such as Linux ext2, ext3, and ext4) instead organize the drive
into block groups, each of which is just a consecutive portion of the disk’s
address space. The picture below illustrates an example wher e every 8
blocks are organized into a different block group (note that real g roups
would consist of many more blocks):
Group 0 Group 1 Group 2
Whether you call them cylinder groups or block groups, these groups
are the central mechanism that FFS uses to improve performance . Crit-
ically , by placing two ﬁles within the same group, FFS can ensu re that
accessing one after the other will not result in long seeks across t he disk.
To use these groups to store ﬁles and directories, FFS needs to ha ve the
ability to place ﬁles and directories into a group, and track al l necessary
information about them therein. To do so, FFS includes all the str uctures
you might expect a ﬁle system to have within each group, e.g., sp ace for
inodes, data blocks, and some structures to track whether each of those
are allocated or free. Here is a depiction of what FFS keeps within a single
cylinder group:
S ib db Inodes Data
Let’s now examine the components of this single cylinder group in
more detail. FFS keeps a copy of the super block (S) in each group for
reliability reasons. The super block is needed to mount the ﬁle s ystem;
by keeping multiple copies, if one copy becomes corrupt, you can sti ll
mount and access the ﬁle system by using a working replica.
Within each group, FFS needs to track whether the inodes and dat a
blocks of the group are allocated. A per-group inode bitmap (ib) and
data bitmap (db) serve this role for inodes and data blocks in each group.
Bitmaps are an excellent way to manage free space in a ﬁle syst em be-
cause it is easy to ﬁnd a large chunk of free space and allocate it to a ﬁle,
perhaps avoiding some of the fragmentation problems of the free lis t in
the old ﬁle system.
Finally , theinode and data block regions are just like those in the pre-
vious very-simple ﬁle system (VSFS). Most of each cylinder group, a s
usual, is comprised of data blocks.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOCALITY AND THE FAST FILE SYSTEM 5
ASIDE : FFS F ILE CREATION
As an example, think about what data structures must be update d when
a ﬁle is created; assume, for this example, that the user creat es a new ﬁle
/foo/bar.txt and that the ﬁle is one block long (4KB). The ﬁle is new,
and thus needs a new inode; thus, both the inode bitmap and the new ly-
allocated inode will be written to disk. The ﬁle also has data in it and
thus it too must be allocated; the data bitmap and a data block wil l thus
(eventually) be written to disk. Hence, at least four writes t o the current
cylinder group will take place (recall that these writes may b e buffered
in memory for a while before they take place). But this is not all! I n
particular, when creating a new ﬁle, you must also place the ﬁl e in the
ﬁle-system hierarchy , i.e., the directory must be updated. Sp eciﬁcally , the
parent directory foo must be updated to add the entry for bar.txt; this
update may ﬁt in an existing data block of foo or require a new block to
be allocated (with associated data bitmap). The inode of foo must also
be updated, both to reﬂect the new length of the directory as well as to
update time ﬁelds (such as last-modiﬁed-time). Overall, it i s a lot of work
just to create a new ﬁle! Perhaps next time you do so, you should be m ore
thankful, or at least surprised that it all works so well.
41.4 Policies: How To Allocate Files and Directories
With this group structure in place, FFS now has to decide how to pl ace
ﬁles and directories and associated metadata on disk to improve p erfor-
mance. The basic mantra is simple: keep related stuff together (and its corol-
lary ,keep unrelated stuff far apart ).
Thus, to obey the mantra, FFS has to decide what is “related” an d
place it within the same block group; conversely , unrelated ite ms should
be placed into different block groups. To achieve this end, FFS makes use
of a few simple placement heuristics.
The ﬁrst is the placement of directories. FFS employs a simple ap -
proach: ﬁnd the cylinder group with a low number of allocated direc -
tories (to balance directories across groups) and a high number of free
inodes (to subsequently be able to allocate a bunch of ﬁles), and put the
directory data and inode in that group. Of course, other heuristic s could
be used here (e.g., taking into account the number of free data b locks).
For ﬁles, FFS does two things. First, it makes sure (in the gener al case)
to allocate the data blocks of a ﬁle in the same group as its inode, th us
preventing long seeks between inode and data (as in the old ﬁle sy stem).
Second, it places all ﬁles that are in the same directory in the cy linder
group of the directory they are in. Thus, if a user creates four ﬁle s, /a/b,
/a/c, /a/d, and /b/f, FFS would try to place the ﬁrst three near one
another (same group) and the fourth far away (in some other group).
Let’s look at an example of such an allocation. In the example, as-
sume that there are only 10 inodes and 10 data blocks in each group ( both
© 2008–26, A RPACI -D USSEAU THREE
EASY
PIECES

6 L OCALITY AND THE FAST FILE SYSTEM
unrealistically small numbers), and that the three director ies (the root di-
rectory /, /a, and /b) and four ﬁles ( /a/c, /a/d, /a/e, /b/f ) are
placed within them per the FFS policies. Assume the regular ﬁl es are each
two blocks in size, and that the directories have just a single b lock of data.
For this ﬁgure, we use the obvious symbols for each ﬁle or directory (i .e.,
/ for the root directory ,a for /a, f for /b/f, and so forth).
group inodes data
0 /--------- /---------
1 acde------ accddee---
2 bf-------- bff-------
3 ---------- ----------
4 ---------- ----------
5 ---------- ----------
6 ---------- ----------
7 ---------- ----------
Note that the FFS policy does two positive things: the data blocks of
each ﬁle are near each ﬁle’s inode, and ﬁles in the same directory are
near one another (namely , /a/c, /a/d, and /a/e are all in Group 1, and
directory /b and its ﬁle /b/f are near one another in Group 2).
In contrast, let’s now look at an inode allocation policy that simply
spreads inodes across groups, trying to ensure that no group’s inod e table
ﬁlls up quickly . The ﬁnal allocation might thus look something lik e this:
group inodes data
0 /--------- /---------
1 a--------- a---------
2 b--------- b---------
3 c--------- cc--------
4 d--------- dd--------
5 e--------- ee--------
6 f--------- ff--------
7 ---------- ----------
As you can see from the ﬁgure, while this policy does indeed keep ﬁl e
(and directory) data near its respective inode, ﬁles within a d irectory are
arbitrarily spread around the disk, and thus name-based local ity is not
preserved. Access to ﬁles /a/c, /a/d, and /a/e now spans three groups
instead of one as per the FFS approach.
The FFS policy heuristics are not based on extensive studies of ﬁl e-
system trafﬁc or anything particularly nuanced; rather, the y are based on
good old-fashioned common sense (isn’t that what CS stands for after
all?)1. Files in a directory are often accessed together: imagine compil-
ing a bunch of ﬁles and then linking them into a single executab le. Be-
1Some people refer to common sense as horse sense , especially people who work regu-
larly with horses. However, we have a feeling that this idiom may be l ost as the “mechanized
horse”, a.k.a. the car, gains in popularity . What will they invent next ? A ﬂying machine??!!
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOCALITY AND THE FAST FILE SYSTEM 7
0 2 4 6 8 10
0%
20%
40%
60%
80%
100%
FFS Locality
Path Difference
Cumulative Frequency
Trace
Random
Figure 41.1: FFS Locality For SEER T races
cause such namespace-based locality exists, FFS will often im prove per-
formance, making sure that seeks between related ﬁles are nic e and short.
41.5 Measuring File Locality
To understand better whether these heuristics make sense, l et’s ana-
lyze some traces of ﬁle system access and see if indeed there is n amespace
locality . For some reason, there doesn’t seem to be a good study of this
topic in the literature.
Speciﬁcally , we’ll use the SEER traces [K94] and analyze how “far
away” ﬁle accesses were from one another in the directory tree. For ex-
ample, if ﬁle f is opened, and then re-opened next in the trace (before
any other ﬁles are opened), the distance between these two opens in the
directory tree is zero (as they are the same ﬁle). If a ﬁle f in directory
dir (i.e., dir/f) is opened, and followed by an open of ﬁle g in the same
directory (i.e., dir/g), the distance between the two ﬁle accesses is one,
as they share the same directory but are not the same ﬁle. Our dis tance
metric, in other words, measures how far up the directory tree you h ave
to travel to ﬁnd the common ancestor of two ﬁles; the closer they are in the
tree, the lower the metric.
Figure 41.1 shows the locality observed in the SEER traces over all
workstations in the SEER cluster over the entirety of all traces. T he graph
plots the difference metric along the x-axis, and shows the cumu lative
percentage of ﬁle opens that were of that difference along the y-a xis.
Speciﬁcally , for the SEER traces (marked “Trace” in the graph), you can
see that about 7% of ﬁle accesses were to the ﬁle that was opened pr evi-
© 2008–26, A RPACI -D USSEAU THREE
EASY
PIECES

8 L OCALITY AND THE FAST FILE SYSTEM
ously , and that nearly 40% of ﬁle accesses were to either the sam e ﬁle or
to one in the same directory (i.e., a difference of zero or one). Thu s, the
FFS locality assumption seems to make sense (at least for these t races).
Interestingly , another 25% or so of ﬁle accesses were to ﬁles tha t had a
distance of two. This type of locality occurs when the user has stru ctured
a set of related directories in a multi-level fashion and consist ently jumps
between them. For example, if a user has a src directory and builds
object ﬁles ( .o ﬁles) into an obj directory , and both of these directories
are sub-directories of a main proj directory , a common access pattern
will be proj/src/foo.c followed by proj/obj/foo.o. The distance
between these two accesses is two, as proj is the common ancestor. FFS
does not capture this type of locality in its policies, and thus more seeki ng
will occur between such accesses.
For comparison, the graph also shows locality for a “Random” trace.
The random trace was generated by selecting ﬁles from within an existing
SEER trace in random order, and calculating the distance metric between
these randomly-ordered accesses. As you can see, there is less n amespace
locality in the random traces, as expected. However, because ev entually
every ﬁle shares a common ancestor (e.g., the root), there is some loc ality ,
and thus random is useful as a comparison point.
41.6 The Large-File Exception
In FFS, there is one important exception to the general policy of ﬁle
placement, and it arises for large ﬁles. Without a different ru le, a large
ﬁle would entirely ﬁll the block group it is ﬁrst placed within (a nd maybe
others). Filling a block group in this manner is undesirable, as it prevents
subsequent “related” ﬁles from being placed within this block group, and
thus may hurt ﬁle-access locality .
Thus, for large ﬁles, FFS does the following. After some number of
blocks are allocated into the ﬁrst block group (e.g., 12 blocks, or t he num-
ber of direct pointers available within an inode), FFS places the next “large”
chunk of the ﬁle (e.g., those pointed to by the ﬁrst indirect block ) in an-
other block group (perhaps chosen for its low utilization). Then, th e next
chunk of the ﬁle is placed in yet another different block group, an d so on.
Let’s look at some diagrams to understand this policy better. With out
the large-ﬁle exception, a single large ﬁle would place all of it s blocks into
one part of the disk. We investigate a small example of a ﬁle ( /a) with 30
blocks in an FFS conﬁgured with 10 inodes and 40 data blocks per grou p.
Here is the depiction of FFS without the large-ﬁle exception:
group inodes data
0 /a-------- /aaaaaaaaa aaaaaaaaaa aaaaaaaaaa a---------
1 ---------- ---------- ---------- ---------- ----------
2 ---------- ---------- ---------- ---------- ----------
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOCALITY AND THE FAST FILE SYSTEM 9
As you can see in the picture, /a ﬁlls up most of the data blocks in
Group 0, whereas other groups remain empty . If some other ﬁles are n ow
created in the root directory ( /), there is not much room for their data in
the group.
With the large-ﬁle exception (here set to ﬁve blocks in each chu nk),
FFS instead spreads the ﬁle across groups, and the resulting ut ilization
within any one group is not too high:
group inodes data
0 /a-------- /aaaaa---- ---------- ---------- ----------
1 ---------- aaaaa----- ---------- ---------- ----------
2 ---------- aaaaa----- ---------- ---------- ----------
3 ---------- aaaaa----- ---------- ---------- ----------
4 ---------- aaaaa----- ---------- ---------- ----------
5 ---------- aaaaa----- ---------- ---------- ----------
6 ---------- ---------- ---------- ---------- ----------
The astute reader (that’s you) will note that spreading blocks of a ﬁle
across the disk will hurt performance, particularly in the rel atively com-
mon case of sequential ﬁle access (e.g., when a user or applicati on reads
chunks 0 through 29 in order). And you are right, oh astute reader of
ours! But you can address this problem by choosing chunk size caref ully .
Speciﬁcally , if the chunk size is large enough, the ﬁle system w ill spend
most of its time transferring data from disk and just a (relative ly) little
time seeking between chunks of the block. This process of reducin g an
overhead by doing more work per overhead paid is called amortization
and is a common technique in computer systems.
Let’s do an example: assume that the average positioning time (i .e.,
seek and rotation) for a disk is 10 ms. Assume further that the dis k trans-
fers data at 40 MB/s. If your goal was to spend half our time seekin g
between chunks and half our time transferring data (and thus a chieve
50% of peak disk performance), you would thus need to spend 10 ms
transferring data for every 10 ms positioning. So the question bec omes:
how big does a chunk have to be in order to spend 10 ms in transfer?
Easy , just use our old friend, math, in particular the dimension al analysis
mentioned in the chapter on disks [AD18a]:
40 ✘ ✘M B
✟✟sec · 1024 KB
1 ✘ ✘M B · 1 ✟✟sec
1000 ✟✟ms ·10 ✟✟ms = 409.6 KB (41.1)
Basically , what this equation says is this: if you transfer dat a at 40
MB/s, you need to transfer only 409.6KB every time you seek in orde r to
spend half your time seeking and half your time transferring. Si milarly ,
you can compute the size of the chunk you would need to achieve 90%
of peak bandwidth (turns out it is about 3.6MB), or even 99% of peak
bandwidth (39.6MB!). As you can see, the closer you want to get to p eak,
the bigger these chunks get (see Figure 41.2 for a plot of these va lues).
FFS did not use this type of calculation in order to spread large ﬁl es
across groups, however. Instead, it took a simple approach, based on the
© 2008–26, A RPACI -D USSEAU THREE
EASY
PIECES

10 L OCALITY AND THE FAST FILE SYSTEM
0% 25% 50% 75% 100%
1K
32K
1M
10M
The Challenges of Amortization
Percent Bandwidth (Desired)
Log(Chunk Size Needed)
50%, 409.6K
90%, 3.69M
Figure 41.2: Amortization: How Big Do Chunks Have T o Be?
structure of the inode itself. The ﬁrst twelve direct blocks wer e placed
in the same group as the inode; each subsequent indirect block, a nd all
the blocks it pointed to, was placed in a different group. With a bl ock
size of 4KB, and 32-bit disk addresses, this strategy implies that every
1024 blocks of the ﬁle (4MB) were placed in separate groups, the l one
exception being the ﬁrst 48KB of the ﬁle as pointed to by direct poi nters.
Note that the trend in disk drives is that transfer rate improve s fairly
rapidly , as disk manufacturers are good at cramming more bits in to the
same surface, but the mechanical aspects of drives related to seeks (disk
arm speed and the rate of rotation) improve rather slowly [P98]. Th e
implication is that over time, mechanical costs become relative ly more
expensive, and thus, to amortize said costs, you have to transfe r more
data between seeks.
41.7 A Few Other Things About FFS
FFS introduced a few other innovations too. In particular, the desi gn-
ers were extremely worried about accommodating small ﬁles; as it turned
out, many ﬁles were 2KB or so in size back then, and using 4KB block s,
while good for transferring data, was not so good for space efﬁciency .
This internal fragmentation could thus lead to roughly half the disk be-
ing wasted for a typical ﬁle system.
The solution the FFS designers hit upon was simple and solved the
problem. They decided to introduce sub-blocks, which were 512-byte
little blocks that the ﬁle system could allocate to ﬁles. Thus, i f you created
a small ﬁle (say 1KB in size), it would occupy two sub-blocks and t hus not
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOCALITY AND THE FAST FILE SYSTEM 11
0
11
1098
7
6
5
4 3 2
1
Spindle
0
11
5104
9
3
8
2 7 1
6
Spindle
Figure 41.3: FFS: Standard V ersus Parameterized Placement
waste an entire 4KB block. As the ﬁle grew, the ﬁle system will c ontinue
allocating 512-byte blocks to it until it acquires a full 4KB of d ata. At that
point, FFS will ﬁnd a 4KB block, copy the sub-blocks into it, and free the
sub-blocks for future use.
You might observe that this process is inefﬁcient, requiring a l ot of ex-
tra work for the ﬁle system (in particular, a lot of extra I/O to per form the
copy). And you’d be right again! Thus, FFS generally avoided this pes-
simal behavior by modifying the libc library; the library would buffer
writes and then issue them in 4KB chunks to the ﬁle system, thu s avoid-
ing the sub-block specialization entirely in most cases.
A second neat thing that FFS introduced was a disk layout that was
optimized for performance. In those times (before SCSI and other more
modern device interfaces), disks were much less sophisticate d and re-
quired the host CPU to control their operation in a more hands-on way .
A problem arose in FFS when a ﬁle was placed on consecutive sectors of
the disk, as on the left in Figure 41.3.
In particular, the problem arose during sequential reads. FFS would
ﬁrst issue a read to block 0; by the time the read was complete, an d FFS
issued a read to block 1, it was too late: block 1 had rotated under t he
head and now the read to block 1 would incur a full rotation.
FFS solved this problem with a different layout, as you can see on th e
right in Figure 41.3. By skipping over every other block (in the e xample),
FFS has enough time to request the next block before it went past t he
disk head. In fact, FFS was smart enough to ﬁgure out for a particu lar
disk how many blocks it should skip in doing layout in order to avoid the
extra rotations; this technique was called parameterization, as FFS would
ﬁgure out the speciﬁc performance parameters of the disk and use those
to decide on the exact staggered layout scheme.
You might be thinking: this scheme isn’t so great after all. In f act, you
will only get 50% of peak bandwidth with this type of layout, becau se
you have to go around each track twice just to read each block once. For-
tunately , modern disks are much smarter: they internally rea d the entire
track in and buffer it in an internal disk cache (often called a track buffer
for this very reason). Then, on subsequent reads to the track, th e disk will
© 2008–26, A RPACI -D USSEAU THREE
EASY
PIECES

12 L OCALITY AND THE FAST FILE SYSTEM
TIP : M AKE THE SYSTEM USABLE
Probably the most basic lesson from FFS is that not only did it intro-
duce the conceptually good idea of disk-aware layout, but it also a dded
a number of features that simply made the system more usable. Lon g ﬁle
names, symbolic links, and a rename operation that worked atomica lly
all improved the utility of a system; while hard to write a resea rch pa-
per about (imagine trying to read a 14-pager about “The Symbolic L ink:
Hard Link’s Long Lost Cousin”), such small features made FFS more u se-
ful and thus likely increased its chances for adoption. Making a system
usable is often as or more important than its deep technical innova tions.
just return the desired data from its cache. File systems thus no longer
have to worry about these incredibly low-level details. Abstra ction and
higher-level interfaces can be a good thing, when designed prop erly .
Some other usability improvements were added as well. FFS was one
of the ﬁrst ﬁle systems to allow for long ﬁle names , thus enabling more
expressive names in the ﬁle system instead of the traditional ﬁ xed-size
approach (e.g., 8 characters). Further, a new concept was intr oduced
called a symbolic link . As discussed in a previous chapter [AD18b] ,
hard links are limited in that they both could not point to director ies (for
fear of introducing loops in the ﬁle system hierarchy) and that th ey can
only point to ﬁles within the same volume (i.e., the inode number m ust
still be meaningful). Symbolic links allow the user to create an “alias” to
any other ﬁle or directory on a system and thus are much more ﬂexible .
FFS also introduced an atomic rename() operation for renaming ﬁles.
Usability improvements, beyond the basic technology , also like ly gained
FFS a stronger user base.
41.8 Summary
The introduction of FFS was a watershed moment in ﬁle system his-
tory , as it made clear that the problem of ﬁle management was one of t he
most interesting issues within an operating system, and showed how one
might begin to deal with that most important of devices, the hard disk.
Since that time, hundreds of new ﬁle systems have developed, but still
today many ﬁle systems take cues from FFS (e.g., Linux ext2 and e xt3 are
obvious intellectual descendants). Certainly all modern syst ems account
for the main lesson of FFS: treat the disk like it’s a disk.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LOCALITY AND THE FAST FILE SYSTEM 13
References
[AD18a] “Operating Systems: Three Easy Pieces” (Chapter: Hard Disk Dr ives) by Remzi
Arpaci-Dusseau and Andrea Arpaci-Dusseau. Arpaci-Dusseau Books, 2 018. There is no way
you should be reading about FFS without having ﬁrst understood hard drives in some detail. If you try
to do so, please instead go directly to jail; do not pass go, and, critically, d o not collect 200 much-needed
simoleons.
[AD18b] “Operating Systems: Three Easy Pieces” (Chapter: File System Implementation) by
Remzi Arpaci-Dusseau and Andrea Arpaci-Dusseau . Arpaci-Dusseau Bo oks, 2018. As above,
it makes little sense to read this chapter unless you have read (and understood) th e chapter on ﬁle
system implementation. Otherwise, we’ll be throwing around terms like “i node” and “indirect block”
and you’ll be like “huh?” and that is no fun for either of us.
[K94] “The Design of the SEER Predictive Caching System” by G. H. Kuenning. MOBICOMM
’94, Santa Cruz, California, December 1994. According to Kuenning, this is the best overview of the
SEER project, which led to (among other things) the collection of these traces.
[MJLF84] “A Fast File System for U NIX ” by Marshall K. McKusick, William N. Joy , Sam J.
Lefﬂer, Robert S. Fabry . ACM TOCS, 2:3, August 1984. McKusick was recently honored with the
IEEE Reynold B. Johnson award for his contributions to ﬁle systems, much of whi ch was based on
his work building FFS. In his acceptance speech, he discussed the ori ginal FFS software: only 1200
lines of code! Modern versions are a little more complex, e.g., the BSD FF S descendant now is in the
50-thousand lines-of-code range.
[P98] “Hardware Technology Trends and Database Opportunities” by Dav id A. Patterson.
Keynote Lecture at SIGMOD ’98, June 1998. A great and simple overview of disk technology trends
and how they change over time.
© 2008–26, A RPACI -D USSEAU THREE
EASY
PIECES

14 L OCALITY AND THE FAST FILE SYSTEM
Homework (Simulation)
This section introduces ffs.py, a simple FFS simulator you can use
to understand better how FFS-based ﬁle and directory allocation w ork.
See the README for details on how to run the simulator.
Questions
1. Examine the ﬁle in.largefile, and then run the simulator with ﬂag -f
in.largefile and -L 4 . The latter sets the large-ﬁle exception to 4 blocks.
What will the resulting allocation look like? Run with -c to check.
2. Now run with -L 30 . What do you expect to see? Once again, turn on -c
to see if you were right. You can also use -S to see exactly which blocks
were allocated to the ﬁle /a.
3. Now we will compute some statistics about the ﬁle. The ﬁrst is so mething
we call ﬁlespan , which is the max distance between any two data blocks of
the ﬁle or between the inode and any data block. Calculate the ﬁ lespan of
/a. Run ffs.py -f in.largefile -L 4 -T -c to see what it is. Do
the same with -L 100 . What difference do you expect in ﬁlespan as the
large-ﬁle exception parameter changes from low values to high v alues?
4. Now let’s look at a new input ﬁle, in.manyfiles. How do you think the
FFS policy will lay these ﬁles out across groups? (you can run wit h -v to
see what ﬁles and directories are created, or just cat in.manyfiles ). Run
the simulator with -c to see if you were right.
5. A metric to evaluate FFS is called dirspan. This metric calculates the spread
of ﬁles within a particular directory , speciﬁcally the max dis tance between
the inodes and data blocks of all ﬁles in the directory and the inode and data
block of the directory itself. Run with in.manyfiles and the -T ﬂag, and
calculate the dirspan of the three directories. Run with -c to check. How
good of a job does FFS do in minimizing dirspan?
6. Now change the size of the inode table per group to 5 ( -i 5 ). How do you
think this will change the layout of the ﬁles? Run with -c to see if you were
right. How does it affect the dirspan?
7. Which group should FFS place inode of a new directory in? The d efault
(simulator) policy looks for the group with the most free inodes. A different
policy looks for a set of groups with the most free inodes. For exa mple, if
you run with -A 2 , when allocating a new directory , the simulator will look
at groups in pairs and pick the best pair for the allocation. Run ./ffs.py
-f in.manyfiles -i 5 -A 2 -c to see how allocation changes with
this strategy . How does it affect dirspan? Why might this poli cy be good?
8. One last policy change we will explore relates to ﬁle fragmen tation. Run
./ffs.py -f in.fragmented -v and see if you can predict how the
ﬁles that remain are allocated. Run with -c to conﬁrm your answer. What
is interesting about the data layout of ﬁle /i? Why is it problematic?
9. A new policy , which we call contiguous allocation (-C), tries to ensure that
each ﬁle is allocated contiguously . Speciﬁcally , with -C n , the ﬁle system
tries to ensure that n contiguous blocks are free within a group before al-
locating a block. Run ./ffs.py -f in.fragmented -v -C 2 -c to
see the difference. How does layout change as the parameter pas sed to -C
increases? Finally , how does -C affect ﬁlespan and dirspan?
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
