Title: file-disks.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/file-disks.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:21+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

37
Hard Disk Drives
The last chapter introduced the general concept of an I/O device and
showed you how the OS might interact with such a beast. In this cha pter,
we dive into more detail about one device in particular: the hard disk
drive. These drives have been the main form of persistent data storage in
computer systems for decades and much of the development of ﬁle sys -
tem technology (coming soon) is predicated on their behavior. Thus, it
is worth understanding the details of a disk’s operation before bui lding
the ﬁle system software that manages it. Many of these details a re avail-
able in excellent papers by Ruemmler and Wilkes [RW92] and An derson,
Dykes, and Riedel [ADR03].
CRUX : H OW TO STORE AND ACCESS DATA ON DISK
How do modern hard-disk drives store data? What is the interface ?
How is the data actually laid out and accessed? How does disk sched ul-
ing improve performance?
37.1 The Interface
Let’s start by understanding the interface to a modern disk dri ve. The
basic interface for all modern drives is straightforward. The drive consists
of a large number of sectors (512-byte blocks), each of which can be read
or written. The sectors are numbered from 0 to n − 1 on a disk with n
sectors. Thus, we can view the disk as an array of sectors; 0 to n − 1 is
thus the address space of the drive.
Multi-sector operations are possible; indeed, many ﬁle systems will
read or write 4KB at a time (or more). However, when updating the di sk,
the only guarantee drive manufacturers make is that a single 5 12-byte
write is atomic (i.e., it will either complete in its entirety or it won’t com-
plete at all); thus, if an untimely power loss occurs, only a portion of a
larger write may complete (sometimes called a torn write).
There are some assumptions most clients of disk drives make, but
that are not speciﬁed directly in the interface; Schlosser and G anger have
1

2 H ARD DISK DRIVES
0
11
1098
7
6
5
4 3 2
1
Spindle
Figure 37.1: A Disk With Just A Single T rack
called this the “unwritten contract” of disk drives [SG04]. Spec iﬁcally ,
one can usually assume that accessing two blocks1 near one-another within
the drive’s address space will be faster than accessing two bl ocks that are
far apart. One can also usually assume that accessing blocks i n a contigu-
ous chunk (i.e., a sequential read or write) is the fastest acce ss mode, and
usually much faster than any more random access pattern.
37.2 Basic Geometry
Let’s start to understand some of the components of a modern disk.
We start with a platter, a circular hard surface on which data is stored
persistently by inducing magnetic changes to it. A disk may h ave one
or more platters; each platter has 2 sides, each of which is calle d a sur-
face. These platters are usually made of some hard material (such as
aluminum), and then coated with a thin magnetic layer that ena bles the
drive to persistently store bits even when the drive is powered off.
The platters are all bound together around the spindle, which is con-
nected to a motor that spins the platters around (while the drive is pow-
ered on) at a constant (ﬁxed) rate. The rate of rotation is often measured in
rotations per minute (RPM) , and typical modern values are in the 7,200
RPM to 15,000 RPM range. Note that we will often be interested in the
time of a single rotation, e.g., a drive that rotates at 10,000 RPM means
that a single rotation takes about 6 milliseconds (6 ms).
Data is encoded on each surface in concentric circles of sectors; w e call
one such concentric circle a track. A single surface contains many thou-
sands and thousands of tracks, tightly packed together, with hu ndreds of
tracks ﬁtting into the width of a human hair.
To read and write from the surface, we need a mechanism that all ows
us to either sense (i.e., read) the magnetic patterns on the di sk or to in-
duce a change in (i.e., write) them. This process of reading and writing is
accomplished by the disk head; there is one such head per surface of the
drive. The disk head is attached to a single disk arm, which moves across
the surface to position the head over the desired track.
1We, and others, often use the terms block and sector interchangeably , assuming the
reader will know exactly what is meant per context. Sorry about this!
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

HARD DISK DRIVES 3
Head
Arm
0
11
1098
7
6
5
4 3 2
1
Spindle
Rotates this way
Figure 37.2: A Single T rack Plus A Head
37.3 A Simple Disk Drive
Let’s understand how disks work by building up a model one track at
a time. Assume we have a simple disk with a single track (Figur e 37.1).
This track has just 12 sectors, each of which is 512 bytes in size (our typical
sector size, recall) and addressed therefore by the numbers 0 t hrough 11.
The single platter we have here rotates around the spindle, to w hich a
motor is attached.
Of course, the track by itself isn’t too interesting; we want to b e able
to read or write those sectors, and thus we need a disk head, attac hed
to a disk arm, as we now see (Figure 37.2). In the ﬁgure, the disk head,
attached to the end of the arm, is positioned over sector 6, and the s urface
is rotating counter-clockwise.
Single-track Latency: The Rotational Delay
To understand how a request would be processed on our simple, one-
track disk, imagine we now receive a request to read block 0. How s hould
the disk service this request?
In our simple disk, the disk doesn’t have to do much. In particula r, it
must just wait for the desired sector to rotate under the disk hea d. This
wait happens often enough in modern drives, and is an important enough
component of I/O service time, that it has a special name: rotational de-
lay (sometimes rotation delay, though that sounds weird). In the exam-
ple, if the full rotational delay is R, the disk has to incur a rotational delay
of about R
2 to wait for 0 to come under the read/write head (if we start at
6). A worst-case request on this single track would be to sector 5, causing
nearly a full rotational delay in order to service such a request .
Multiple T racks: Seek Time
So far our disk just has a single track, which is not too realistic; modern
disks of course have many millions. Let’s thus look at an ever-so-sli ghtly
more realistic disk surface, this one with three tracks (Figur e 37.3, left).
In the ﬁgure, the head is currently positioned over the innermost track
(which contains sectors 24 through 35); the next track over contai ns the
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

4 H ARD DISK DRIVES
0
11
10
9
8
7
6
5
4
3
2
1
12
23
222120
19
18
17
16 15 14
13
24
35
343332
31
30
29
28 27 26
25
Spindle
Rotates this way
SeekRemaining rotation
3
2
1
0
11
10
9
8
7
6
5
4
15
14
131223
22
21
20
19 18 17
16
27
26
252435
34
33
32
31 30 29
28
Spindle
Rotates this way
Figure 37.3: Three T racks Plus A Head (Right: With Seek)
next set of sectors (12 through 23), and the outermost track contain s the
ﬁrst sectors (0 through 11).
To understand how the drive might access a given sector, we now trace
what would happen on a request to a distant sector, e.g., a read to sector
11. To service this read, the drive has to ﬁrst move the disk arm to the cor-
rect track (in this case, the outermost one), in a process known as a seek.
Seeks, along with rotations, are one of the most costly disk operations.
The seek, it should be noted, has many phases: ﬁrst an acceleration
phase as the disk arm gets moving; then coasting as the arm is moving
at full speed, then deceleration as the arm slows down; ﬁnally settling as
the head is carefully positioned over the correct track. The settling time
is often quite signiﬁcant, e.g., 0.5 to 2 ms, as the drive must b e certain to
ﬁnd the right track (imagine if it just got close instead!).
After the seek, the disk arm has positioned the head over the righ t
track. A depiction of the seek is found in Figure 37.3 (right).
As we can see, during the seek, the arm has been moved to the desi red
track, and the platter of course has rotated, in this case about 3 s ectors.
Thus, sector 9 is just about to pass under the disk head, and we mu st
only endure a short rotational delay to complete the transfer.
When sector 11 passes under the disk head, the ﬁnal phase of I/O
will take place, known as the transfer, where data is either read from or
written to the surface. And thus, we have a complete picture of I /O time:
ﬁrst a seek, then waiting for the rotational delay , and ﬁnally th e transfer.
Some Other Details
Though we won’t spend too much time on it, there are some other inter-
esting details about how hard drives operate. Many drives employ some
kind of track skew to make sure that sequential reads can be properly
serviced even when crossing track boundaries. In our simple exa mple
disk, this might appear as seen in Figure 37.4 (page 5).
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

HARD DISK DRIVES 5
Track skew: 2 blocks
0
11
10
9
8
7
6
5
4
3
2
1
22
21
201918
17
16
15
14 13 12
23
32
31
302928
27
26
25
24 35 34
33
Spindle
Rotates this way
Figure 37.4: Three T racks: T rack Skew Of 2
Sectors are often skewed like this because when switching from one
track to another, the disk needs time to reposition the head (even to neigh-
boring tracks). Without such skew, the head would be moved to the n ext
track but the desired next block would have already rotated unde r the
head, and thus the drive would have to wait almost the entire rota tional
delay to access the next block.
Another reality is that outer tracks tend to have more sectors tha n
inner tracks, which is a result of geometry; there is simply more room
out there. These tracks are often referred to as multi-zoned disk drives,
where the disk is organized into multiple zones, and where a zone is con-
secutive set of tracks on a surface. Each zone has the same number of
sectors per track, and outer zones have more sectors than inner zone s.
Finally , an important part of any modern disk drive is its cache, for
historical reasons sometimes called a track buffer. This cache is just some
small amount of memory (usually around 8 or 16 MB) which the drive
can use to hold data read from or written to the disk. For example, w hen
reading a sector from the disk, the drive might decide to read in all of the
sectors on that track and cache them in its memory; doing so allows t he
drive to quickly respond to any subsequent requests to the sam e track.
On writes, the drive has a choice: should it acknowledge the writ e has
completed when it has put the data in its memory , or after the writ e has
actually been written to disk? The former is called write back caching
(or sometimes immediate reporting), and the latter write through. Write
back caching sometimes makes the drive appear “faster”, but c an be dan-
gerous; if the ﬁle system or applications require that data be wr itten to
disk in a certain order for correctness, write-back caching can lead to
problems (read the chapter on ﬁle-system journaling for details ).
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

6 H ARD DISK DRIVES
ASIDE : D IMENSIONAL ANALYSIS
Remember in Chemistry class, how you solved virtually every prob lem
by simply setting up the units such that they canceled out, and somehow
the answers popped out as a result? That chemical magic is known b y the
highfalutin name of dimensional analysis and it turns out it is useful in
computer systems analysis too.
Let’s do an example to see how dimensional analysis works and why i t is
useful. In this case, assume you have to ﬁgure out how long, in mill isec-
onds, a single rotation of a disk takes. Unfortunately , you are give n only
the RPM of the disk, or rotations per minute. Let’s assume we’re talking
about a 10K RPM disk (i.e., it rotates 10,000 times per minute). How do
we set up the dimensional analysis so that we get time per rotati on in
milliseconds?
To do so, we start by putting the desired units on the left; in thi s case,
we wish to obtain the time (in milliseconds) per rotation, so that is ex-
actly what we write down: T ime (ms)
1 Rotation . We then write down everything
we know, making sure to cancel units where possible. First, we ob tain
1 minute
10,000 Rotations (keeping rotation on the bottom, as that’s where it is on
the left), then transform minutes into seconds with 60 seconds
1 minute , and then
ﬁnally transform seconds in milliseconds with 1000 ms
1 second . The ﬁnal result is
the following (with units nicely canceled):
T ime (ms)
1 Rot. = 1 ✘ ✘ ✘minute
10,000 Rot. · 60 ✘ ✘ ✘seconds
1 ✘ ✘ ✘minute · 1000 ms
1 ✘ ✘✘second = 60,000 ms
10,000 Rot. = 6 ms
Rotation
As you can see from this example, dimensional analysis makes wha t
seems intuitive into a simple and repeatable process. Beyond t he
RPM calculation above, it comes in handy with I/O analysis regul arly .
For example, you will often be given the transfer rate of a disk, e. g.,
100 MB/second, and then asked: how long does it take to transfer a
512 KB block (in milliseconds)? With dimensional analysis, it’s easy:
T ime (ms)
1 Request = 512 ✟✟KB
1 Request · 1 ✟✟M B
1024 ✟✟KB · 1 ✘ ✘✘second
100 ✟✟M B · 1000 ms
1 ✘ ✘✘second = 5 ms
Request
37.4 I/O Time: Doing The Math
Now that we have an abstract model of the disk, we can use a little
analysis to better understand disk performance. In particul ar, we can
now represent I/O time as the sum of three major components:
TI/O = Tseek + Trotation + Ttransf er (37.1)
Note that the rate of I/O ( RI/O ), which is often more easily used for
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

HARD DISK DRIVES 7
Cheetah 15K.5 Barracuda
Capacity 300 GB 1 TB
RPM 15,000 7,200
Average Seek 4 ms 9 ms
Max Transfer 125 MB/s 105 MB/s
Platters 4 4
Cache 16 MB 16/32 MB
Connects via SCSI SATA
Figure 37.5: Disk Drive Specs: SCSI V ersus SATA
comparison between drives (as we will do below), is easily comput ed
from the time. Simply divide the size of the transfer by the time i t took:
RI/O = Size T ransf er
TI/O
(37.2)
To get a better feel for I/O time, let us perform the following calc u-
lation. Assume there are two workloads we are interested in. The ﬁrst,
known as the random workload, issues small (e.g., 4KB) reads to random
locations on the disk. Random workloads are common in many impor-
tant applications, including database management systems. The second,
known as the sequential workload, simply reads a large number of sec-
tors consecutively from the disk, without jumping around. Sequent ial
access patterns are quite common and thus important as well.
To understand the difference in performance between random an d se-
quential workloads, we need to make a few assumptions about the di sk
drive ﬁrst. Let’s look at a couple of modern disks from Seagate. The ﬁrs t,
known as the Cheetah 15K.5 [S09b], is a high-performance SCSI driv e.
The second, the Barracuda [S09a], is a drive built for capacity . Details on
both are found in Figure 37.5.
As you can see, the drives have quite different characteristi cs, and
in many ways nicely summarize two important components of the dis k
drive market. The ﬁrst is the “high performance” drive market , where
drives are engineered to spin as fast as possible, deliver low s eek times,
and transfer data quickly . The second is the “capacity” marke t, where
cost per byte is the most important aspect; thus, the drives are s lower but
pack as many bits as possible into the space available.
From these numbers, we can start to calculate how well the drive s
would do under our two workloads outlined above. Let’s start by looking
at the random workload. Assuming each 4 KB read occurs at a random
location on disk, we can calculate how long each such read would take .
On the Cheetah:
Tseek = 4 ms, T rotation = 2 ms, T transf er = 30 microsecs (37.3)
The average seek time (4 milliseconds) is just taken as the average time
reported by the manufacturer; note that a full seek (from one end of the
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

8 H ARD DISK DRIVES
TIP : U SE DISKS SEQUENTIALLY
When at all possible, transfer data to and from disks in a sequen tial man-
ner. If sequential is not possible, at least think about transfe rring data
in large chunks: the bigger, the better. If I/O is done in littl e random
pieces, I/O performance will suffer dramatically . Also, user s will suffer.
Also, you will suffer, knowing what suffering you have wrought wit h
your careless random I/Os.
surface to the other) would likely take two or three times longer. The
average rotational delay is calculated from the RPM directly . 1 5000 RPM
is equal to 250 RPS (rotations per second); thus, each rotation tak es 4 ms.
On average, the disk will encounter a half rotation and thus 2 ms i s the
average time. Finally , the transfer time is just the size of th e transfer over
the peak transfer rate; here it is vanishingly small (30 microseconds; note
that we need 1000 microseconds just to get 1 millisecond!).
Thus, from our equation above, TI/O for the Cheetah roughly equals
6 ms. To compute the rate of I/O, we just divide the size of the tran sfer
by the average time, and thus arrive at RI/O for the Cheetah under the
random workload of about 0.66 MB/s. The same calculation for the Bar-
racuda yields a TI/O of about 13.2 ms, more than twice as slow, and thus
a rate of about 0.31 MB/s.
Now let’s look at the sequential workload. Here we can assume there
is a single seek and rotation before a very long transfer. For simpl icity ,
assume the size of the transfer is 100 MB. Thus, TI/O for the Cheetah and
Barracuda is about 800 ms and 950 ms, respectively . The rates of I/O
are thus very nearly the peak transfer rates of 125 MB/s and 105 MB/s,
respectively . Figure 37.6 summarizes these numbers.
Cheetah Barracuda
RI/O Random 0.66 MB/s 0.31 MB/s
RI/O Sequential 125 MB/s 105 MB/s
Figure 37.6: Disk Drive Performance: SCSI V ersus SATA
The ﬁgure shows us a number of important things. First, and most
importantly , there is a huge gap in drive performance between r andom
and sequential workloads, almost a factor of 200 or so for the Cheetah
and more than a factor 300 difference for the Barracuda. And thus we
arrive at the most obvious design tip in the history of computing.
A second, more subtle point: there is a large difference in perfor mance
between high-end “performance” drives and low-end “capacity ” drives.
For this reason (and others), people are often willing to pay top doll ar for
the former while trying to get the latter as cheaply as possible .
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

HARD DISK DRIVES 9
ASIDE : C OMPUTING THE “AVERAGE ” S EEK
In many books and papers, you will see average disk-seek time cit ed
as being roughly one-third of the full seek time. Where does this c ome
from?
Turns out it arises from a simple calculation based on average see k
distance, not time. Imagine the disk as a set of tracks, from 0 to N . The
seek distance between any two tracks x and y is thus computed as the
absolute value of the difference between them: |x − y|.
To compute the average seek distance, all you need to do is to ﬁrs t add
up all possible seek distances:
N∑
x=0
N∑
y=0
|x − y|. (37.4)
Then, divide this by the number of different possible seeks: N 2. To
compute the sum, we’ll just use the integral form:
∫ N
x=0
∫ N
y=0
|x − y| dy dx. (37.5)
To compute the inner integral, let’s break out the absolute value :
∫ x
y=0
(x − y) dy +
∫ N
y=x
(y − x) dy. (37.6)
Solving this leads to (xy − 1
2 y2)
⏐
⏐x
0 + ( 1
2 y2 − xy)
⏐
⏐N
x which can be sim-
pliﬁed to (x2 − N x + 1
2 N 2). Now we have to compute the outer integral:
∫ N
x=0
(x2 − N x + 1
2 N 2) dx, (37.7)
which results in:
( 1
3 x3 − N
2 x2 + N 2
2 x)
⏐
⏐
⏐
⏐
N
0
= N 3
3 . (37.8)
Remember that we still have to divide by the total number of seek s
(N 2) to compute the average seek distance: ( N 3
3 )/(N 2) = 1
3 N . Thus the
average seek distance on a disk, over all possible seeks, is one-t hird the
full distance. And now when you hear that an average seek is one-t hird
of a full seek, you’ll know where it came from.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

10 H ARD DISK DRIVES
0
11
10
9
8
7
6
5
4
3
2
1
12
23
222120
19
18
17
16 15 14
13
24
35
343332
31
30
29
28 27 26
25
Spindle
Rotates this way
Figure 37.7: SSTF: Scheduling Requests 21 And 2
37.5 Disk Scheduling
Because of the high cost of I/O, the OS has historically played a rol e in
deciding the order of I/Os issued to the disk. More speciﬁcally , given a
set of I/O requests, the disk scheduler examines the requests and decides
which one to schedule next [SCO90, JW91].
Unlike job scheduling, where the length of each job is usually un -
known, with disk scheduling, we can make a good guess at how long
a “job” (i.e., disk request) will take. By estimating the seek and possi-
ble rotational delay of a request, the disk scheduler can know how l ong
each request will take, and thus (greedily) pick the one that w ill take the
least time to service ﬁrst. Thus, the disk scheduler will try to follow the
principle of SJF (shortest job ﬁrst) in its operation.
SSTF: Shortest Seek Time First
One early disk scheduling approach is known as shortest-seek-time-ﬁrst
(SSTF) (also called shortest-seek-ﬁrst or SSF). SSTF orders the queue of
I/O requests by track, picking requests on the nearest track t o complete
ﬁrst. For example, assuming the current position of the head is ove r the
inner track, and we have requests for sectors 21 (middle track) and 2
(outer track), we would then issue the request to 21 ﬁrst, wait f or it to
complete, and then issue the request to 2 (Figure 37.7).
SSTF works well in this example, seeking to the middle track ﬁrst and
then the outer track. However, SSTF is not a panacea, for the following
reasons. First, the drive geometry is not available to the host OS; rather,
it sees an array of blocks. Fortunately , this problem is rather ea sily ﬁxed.
Instead of SSTF, an OS can simply implement nearest-block-ﬁrst (NBF),
which schedules the request with the nearest block address ne xt.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

HARD DISK DRIVES 11
The second problem is more fundamental: starvation. Imagine in
our example above if there were a steady stream of requests to the in-
ner track, where the head currently is positioned. Requests to any other
tracks would then be ignored completely by a pure SSTF approach. And
thus the crux of the problem:
CRUX : H OW TO HANDLE DISK STARVATION
How can we implement SSTF-like scheduling but avoid starvation?
Elevator (a.k.a. SCAN or C-SCAN)
The answer to this query was developed some time ago (see [CKR72 ]
for example), and is relatively straightforward. The algorith m, originally
called SCAN, simply moves back and forth across the disk servicing re-
quests in order across the tracks. Let’s call a single pass across the disk
(from outer to inner tracks, or inner to outer) a sweep. Thus, if a request
comes for a block on a track that has already been serviced on this sw eep
of the disk, it is not handled immediately , but rather queued until the next
sweep (in the other direction).
SCAN has a number of variants, all of which do about the same thing.
For example, Coffman et al. introduced F-SCAN, which freezes the queue
to be serviced when it is doing a sweep [CKR72]; this action plac es re-
quests that come in during the sweep into a queue to be serviced later.
Doing so avoids starvation of far-away requests, by delaying the servic-
ing of late-arriving (but nearer by) requests.
C-SCAN is another common variant, short for Circular SCAN . In-
stead of sweeping in both directions across the disk, the algorith m only
sweeps from outer-to-inner, and then resets at the outer track to begin
again. Doing so is a bit more fair to inner and outer tracks, as pur e back-
and-forth SCAN favors the middle tracks, i.e., after servicing the outer
track, SCAN passes through the middle twice before coming back to the
outer track again.
For reasons that should now be clear, the SCAN algorithm (and its
cousins) is sometimes referred to as the elevator algorithm, because it
behaves like an elevator which is either going up or down and not jus t
servicing requests to ﬂoors based on which ﬂoor is closer. Imagine h ow
annoying it would be if you were going down from ﬂoor 10 to 1, and
somebody got on at 3 and pressed 4, and the elevator went up to 4 be-
cause it was “closer” than 1! As you can see, the elevator algorith m, when
used in real life, prevents ﬁghts from taking place on elevators . In disks,
it just prevents starvation.
Unfortunately , SCAN and its cousins do not represent the best schedul-
ing technology . In particular, SCAN (or SSTF even) does not actually a d-
here as closely to the principle of SJF as they could. In particula r, they
ignore rotation. And thus, another crux:
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

12 H ARD DISK DRIVES
CRUX : H OW TO ACCOUNT FOR DISK ROTATION COSTS
How can we implement an algorithm that more closely approximates SJ F
by taking both seek and rotation into account?
SPTF: Shortest Positioning Time First
Before discussing shortest positioning time ﬁrst or SPTF scheduling (some-
times also called shortest access time ﬁrst or SATF), which is the solution
to our problem, let us make sure we understand the problem in more d e-
tail. Figure 37.8 presents an example.
In the example, the head is currently positioned over sector 30 on t he
inner track. The scheduler thus has to decide: should it sched ule sector 16
(on the middle track) or sector 8 (on the outer track) for its next req uest.
So which should it service next?
The answer, of course, is “it depends”. In engineering, it turn s out
“it depends” is almost always the answer, reﬂecting that trad e-offs are
part of the life of the engineer; such maxims are also good in a pinc h,
e.g., when you don’t know an answer to your boss’s question, you might
want to try this gem. However, it is almost always better to know why it
depends, which is what we discuss here.
What it depends on here is the relative time of seeking as compare d
to rotation. If, in our example, seek time is much higher than rota tional
delay , then SSTF (and variants) are just ﬁne. However, imagine i f seek is
quite a bit faster than rotation. Then, in our example, it would ma ke more
sense to seek further to service request 8 on the outer track than it would
to perform the shorter seek to the middle track to service 16, wh ich has to
rotate all the way around before passing under the disk head.
0
11
10
9
8
7
6
5
4
3
2
1
12
23
222120
19
18
17
16 15 14
13
24
35
343332
31
30
29
28 27 26
25
Spindle
Rotates this way
Figure 37.8: SSTF: Sometimes Not Good Enough
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

HARD DISK DRIVES 13
TIP : I T ALWAYS DEPENDS (L IVNY ’ S LAW)
Almost any question can be answered with “it depends”, as our colleague
Miron Livny always says. However, use with caution, as if you answ er
too many questions this way , people will stop asking you questions a lto-
gether. For example, somebody asks: “want to go to lunch?” You rep ly:
“it depends, are you coming along?”
On modern drives, as we saw above, both seek and rotation are roughly
equivalent (depending, of course, on the exact requests), and t hus SPTF
is useful and improves performance. However, it is even more difﬁ cult
to implement in an OS, which generally does not have a good idea wher e
track boundaries are or where the disk head currently is (in a rot ational
sense). Thus, SPTF is usually performed inside a drive, descri bed below.
Other Scheduling Issues
There are many other issues we do not discuss in this brief descr iption
of basic disk operation, scheduling, and related topics. One suc h is-
sue is this: where is disk scheduling performed on modern systems? In
older systems, the operating system did all the scheduling; af ter looking
through the set of pending requests, the OS would pick the best one , and
issue it to the disk. When that request completed, the next one w ould be
chosen, and so forth. Disks were simpler then, and so was life.
In modern systems, disks can accommodate multiple outstanding r e-
quests, and have sophisticated internal schedulers themselves (which can
implement SPTF accurately; inside the disk controller, all rel evant details
are available, including exact head position). Thus, the OS sc heduler usu-
ally picks what it thinks the best few requests are (say 16) and issues them
all to disk; the disk then uses its internal knowledge of head pos ition and
detailed track layout information to service said requests in t he best pos-
sible (SPTF) order.
Another important related task performed by disk schedulers is I/O
merging. For example, imagine a series of requests to read blocks 33,
then 8, then 34, as in Figure 37.8. In this case, the scheduler should merge
the requests for blocks 33 and 34 into a single two-block request; any re-
ordering that the scheduler does is performed upon the merged req uests.
Merging is particularly important at the OS level, as it reduc es the num-
ber of requests sent to the disk and thus lowers overheads.
One ﬁnal problem that modern schedulers address is this: how long
should the system wait before issuing an I/O to disk? One might n aively
think that the disk, once it has even a single I/O, should immedi ately
issue the request to the drive; this approach is called work-conserving, as
the disk will never be idle if there are requests to serve. However, research
on anticipatory disk scheduling has shown that sometimes it is better to
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

14 H ARD DISK DRIVES
wait for a bit [ID01], in what is called a non-work-conserving approach.
By waiting, a new and “better” request may arrive at the disk, and thus
overall efﬁciency is increased. Of course, deciding when to wa it, and for
how long, can be tricky; see the research paper for details, or che ck out
the Linux kernel implementation to see how such ideas are trans itioned
into practice (if you are the ambitious sort).
37.6 Summary
We have presented a summary of how disks work. The summary is
actually a detailed functional model; it does not describe the am azing
physics, electronics, and material science that goes into act ual drive de-
sign. For those interested in even more details of that nature, we suggest
a different major (or perhaps minor); for those that are happy with this
model, good! We can now proceed to using the model to build more in-
teresting systems on top of these incredible devices.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

HARD DISK DRIVES 15
References
[ADR03] “More Than an Interface: SCSI vs. ATA” by Dave Anderson, Jim Dyke s, Erik Riedel.
FAST ’03, 2003. One of the best recent-ish references on how modern disk drives really work; a must
read for anyone interested in knowing more.
[CKR72] “Analysis of Scanning Policies for Reducing Disk Seek Times” E.G . Coffman, L.A.
Klimko, B. Ryan SIAM Journal of Computing, September 1972, V ol 1 . No 3. Some of the early
work in the ﬁeld of disk scheduling.
[HK+17] “The Unwritten Contract of Solid State Drives” by Jun He, Sudarsun Kannan, Andrea
C. Arpaci-Dusseau, Remzi H. Arpaci-Dusseau. EuroSys ’17, Belgr ade, Serbia, April 2017. We
take the idea of the unwritten contract, and extend it to SSDs. Using SSDs well s eems as complicated
as hard drives, and sometimes more so.
[ID01] “Anticipatory Scheduling: A Disk-scheduling Framework To Overcome Deceptive Idle-
ness In Synchronous I/O” by Sitaram Iyer, Peter Druschel. SOSP ’01, Octobe r 2001. A cool paper
showing how waiting can improve disk scheduling: better requests may be on their way!
[JW91] “Disk Scheduling Algorithms Based On Rotational Position” by D. Jacobson, J. Wilkes.
Technical Report HPL-CSP-91-7rev1, Hewlett-Packard, February 1991. A more modern take on
disk scheduling. It remains a technical report (and not a published pap er) because the authors were
scooped by Seltzer et al. [SCO90].
[RW92] “An Introduction to Disk Drive Modeling” by C. Ruemmler, J. Wilkes. IEEE Computer,
27:3, March 1994. A terriﬁc introduction to the basics of disk operation. Some pieces are out of date,
but most of the basics remain.
[SCO90] “Disk Scheduling Revisited” by Margo Seltzer, Peter Chen, John Ousterhout. USENIX
1990. A paper that talks about how rotation matters too in the world of disk scheduling.
[SG04] “MEMS-based storage devices and standard disk interfaces: A squ are peg in a round
hole?” Steven W. Schlosser, Gregory R. Ganger FAST ’04, pp. 87-100, 2004 While the MEMS
aspect of this paper hasn’t yet made an impact, the discussion of the contract be tween ﬁle systems and
disks is wonderful and a lasting contribution. We later build on this work to stu dy the “Unwritten
Contract of Solid State Drives” [HK+17]
[S09a] “Barracuda ES.2 data sheet” by Seagate, Inc.. Available at this website, at least, it was:
http://www.seagate.com/docs/pdf/datasheet/disc/ds_barracuda_es.pdf. A
data sheet; read at your own risk. Risk of what? Boredom.
[S09b] “Cheetah 15K.5” by Seagate, Inc.. Available at this websit e, we’re pretty sure it is:
http://www.seagate.com/docs/pdf/datasheet/disc/ds-cheetah-15k-5-us.pdf.
See above commentary on data sheets.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

16 H ARD DISK DRIVES
Homework (Simulation)
This homework uses disk.py to familiarize you with how a modern
hard drive works. It has a lot of different options, and unlike most of
the other simulations, has a graphical animator to show you exactl y what
happens when the disk is in action. See the README for details.
1. Compute the seek, rotation, and transfer times for the follow ing sets of re-
quests: -a 0 , -a 6 , -a 30 , -a 7,30,8 , and ﬁnally -a 10,11,12,13 .
2. Do the same requests above, but change the seek rate to differe nt values: -S
2, -S 4 , -S 8 , -S 10 , -S 40 , -S 0.1 . How do the times change?
3. Do the same requests above, but change the rotation rate: -R 0.1 , -R 0.5 ,
-R 0.01 . How do the times change?
4. FIFO is not always best, e.g., with the request stream -a 7,30,8 , what or-
der should the requests be processed in? Run the shortest seek-t ime ﬁrst
(SSTF) scheduler ( -p SSTF ) on this workload; how long should it take
(seek, rotation, transfer) for each request to be served?
5. Now use the shortest access-time ﬁrst (SATF) scheduler ( -p SATF ). Does it
make any difference for -a 7,30,8 workload? Find a set of requests where
SATF outperforms SSTF; more generally , when is SATF better than SSTF?
6. Here is a request stream to try: -a 10,11,12,13 . What goes poorly when
it runs? Try adding track skew to address this problem ( -o skew ). Given
the default seek rate, what should the skew be to maximize performan ce?
What about for different seek rates (e.g., -S 2 , -S 4 )? In general, could
you write a formula to ﬁgure out the skew?
7. Specify a disk with different density per zone, e.g., -z 10,20,30 , which
speciﬁes the angular difference between blocks on the outer, mi ddle, and
inner tracks. Run some random requests (e.g., -a -1 -A 5,-1,0 , which
speciﬁes that random requests should be used via the -a -1 ﬂag and that
ﬁve requests ranging from 0 to the max be generated), and compute t he
seek, rotation, and transfer times. Use different random seed s. What is the
bandwidth (in sectors per unit time) on the outer, middle, and inn er tracks?
8. A scheduling window determines how many requests the disk can e xamine
at once. Generate random workloads (e.g., -A 1000,-1,0 , with different
seeds) and see how long the SATF scheduler takes when the scheduling win-
dow is changed from 1 up to the number of requests. How big of a windo w
is needed to maximize performance? Hint: use the -c ﬂag and don’t turn
on graphics ( -G) to run these quickly . When the scheduling window is set
to 1, does it matter which policy you are using?
9. Create a series of requests to starve a particular request, as suming an SATF
policy . Given that sequence, how does it perform if you use a bounded
SATF (BSATF) scheduling approach? In this approach, you specify the
scheduling window (e.g., -w 4 ); the scheduler only moves onto the next
window of requests when all requests in the current window have been ser-
viced. Does this solve starvation? How does it perform, as comp ared to
SATF? In general, how should a disk make this trade-off between perfor-
mance and starvation avoidance?
10. All the scheduling policies we have looked at thus far are greedy; they pick
the next best option instead of looking for an optimal schedule. Can you
ﬁnd a set of requests in which greedy is not optimal?
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
