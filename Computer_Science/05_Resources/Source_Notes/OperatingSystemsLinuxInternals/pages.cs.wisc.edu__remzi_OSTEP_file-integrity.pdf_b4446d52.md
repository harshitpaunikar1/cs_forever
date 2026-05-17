Title: file-integrity.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/file-integrity.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:27+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

45
Data Integrity and Protection
Beyond the basic advances found in the ﬁle systems we have studied thus
far, a number of features are worth studying. In this chapter, w e focus on
reliability once again (having previously studied storage sys tem reliabil-
ity in the RAID chapter). Speciﬁcally , how should a ﬁle system or s torage
system ensure that data is safe, given the unreliable nature of modern
storage devices?
This general area is referred to as data integrity or data protection .
Thus, we will now investigate techniques used to ensure that t he data
you put into your storage system is the same when the storage syste m
returns it to you.
CRUX : H OW TO ENSURE DATA INTEGRITY
How should systems ensure that the data written to storage is pro-
tected? What techniques are required? How can such technique s be made
efﬁcient, with both low space and time overheads?
45.1 Disk Failure Modes
As you learned in the chapter about RAID, disks are not perfect, a nd
can fail (on occasion). In early RAID systems, the model of failure was
quite simple: either the entire disk is working, or it fails comp letely , and
the detection of such a failure is straightforward. This fail-stop model of
disk failure makes building RAID relatively simple [S90].
What you didn’t learn is about all of the other types of failure modes
modern disks exhibit. Speciﬁcally , as Bairavasundaram et al. studied
in great detail [B+07, B+08], modern disks will occasionally se em to be
mostly working but have trouble successfully accessing one or moreblocks.
Speciﬁcally , two types of single-block failures are common and worthy of
consideration: latent sector errors (LSEs) and block corruption . We’ll
now discuss each in more detail.
1

2 D ATA INTEGRITY AND PROTECTION
Cheap Costly
LSEs 9.40% 1.40%
Corruption 0.50% 0.05%
Figure 45.1: Frequency Of LSEs And Block Corruption
LSEs arise when a disk sector (or group of sectors) has been damaged
in some way . For example, if the disk head touches the surface for s ome
reason (a head crash , something which shouldn’t happen during nor-
mal operation), it may damage the surface, making the bits unre adable.
Cosmic rays can also ﬂip bits, leading to incorrect contents. For tunately ,
in-disk error correcting codes (ECC) are used by the drive to determine
whether the on-disk bits in a block are good, and in some cases, to ﬁx
them; if they are not good, and the drive does not have enough informa-
tion to ﬁx the error, the disk will return an error when a request i s issued
to read them.
There are also cases where a disk block becomes corrupt in a way not
detectable by the disk itself. For example, buggy disk ﬁrmware may write
a block to the wrong location; in such a case, the disk ECC indicate s the
block contents are ﬁne, but from the client’s perspective the wron g block
is returned when subsequently accessed. Similarly , a block ma y get cor-
rupted when it is transferred from the host to the disk across a fa ulty bus;
the resulting corrupt data is stored by the disk, but it is not what the client
desires. These types of faults are particularly insidious bec ause they are
silent faults; the disk gives no indication of the problem when returning
the faulty data.
Prabhakaran et al. describes this more modern view of disk failu re as
the fail-partial disk failure model [P+05]. In this view, disks can still fail
in their entirety (as was the case in the traditional fail-stop model); how-
ever, disks can also seemingly be working and have one or more block s
become inaccessible (i.e., LSEs) or hold the wrong contents (i.e., corrup-
tion). Thus, when accessing a seemingly-working disk, once in a while
it may either return an error when trying to read or write a given block
(a non-silent partial fault), and once in a while it may simply r eturn the
wrong data (a silent partial fault).
Both of these types of faults are somewhat rare, but just how rare? F ig-
ure 45.1 summarizes some of the ﬁndings from the two Bairavasund aram
studies [B+07,B+08].
The ﬁgure shows the percent of drives that exhibited at least one LSE
or block corruption over the course of the study (about 3 years, over
1.5 million disk drives). The ﬁgure further sub-divides the r esults into
“cheap” drives (usually SATA drives) and “costly” drives (usu ally SCSI
or Fibre Channel). As you can see, while buying better drives re duces
the frequency of both types of problem (by about an order of magnitude ),
they still happen often enough that you need to think carefully about how
to handle them in your storage system.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DATA INTEGRITY AND PROTECTION 3
Some additional ﬁndings about LSEs are:
• Costly drives with more than one LSE are as likely to develop ad-
ditional errors as cheaper drives
• For most drives, annual error rate increases in year two
• The number of LSEs increase with disk size
• Most disks with LSEs have less than 50
• Disks with LSEs are more likely to develop additional LSEs
• There exists a signiﬁcant amount of spatial and temporal locali ty
• Disk scrubbing is useful (most LSEs were found this way)
Some ﬁndings about corruption:
• Chance of corruption varies greatly across different drive mode ls
within the same drive class
• Age effects are different across models
• Workload and disk size have little impact on corruption
• Most disks with corruption only have a few corruptions
• Corruption is not independent within a disk or across disks in RAI D
• There exists spatial locality , and some temporal locality
• There is a weak correlation with LSEs
To learn more about these failures, you should likely read the orig inal
papers [B+07,B+08]. But hopefully the main point should be clea r: if you
really wish to build a reliable storage system, you must includ e machin-
ery to detect and recover from both LSEs and block corruption.
45.2 Handling Latent Sector Errors
Given these two new modes of partial disk failure, we should now tr y
to see what we can do about them. Let’s ﬁrst tackle the easier of th e two,
namely latent sector errors.
CRUX : H OW TO HANDLE LATENT SECTOR ERRORS
How should a storage system handle latent sector errors? How much
extra machinery is needed to handle this form of partial failur e?
As it turns out, latent sector errors are rather straightforward to han-
dle, as they are (by deﬁnition) easily detected. When a storage system
tries to access a block, and the disk returns an error, the storag e system
should simply use whatever redundancy mechanism it has to ret urn the
correct data. In a mirrored RAID, for example, the system should a ccess
the alternate copy; in a RAID-4 or RAID-5 system based on parity , the
system should reconstruct the block from the other blocks in the par ity
group. Thus, easily detected problems such as LSEs are readily r ecovered
through standard redundancy mechanisms.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

4 D ATA INTEGRITY AND PROTECTION
The growing prevalence of LSEs has inﬂuenced RAID designs over the
years. One particularly interesting problem arises in RAID- 4/5 systems
when both full-disk faults and LSEs occur in tandem. Speciﬁcally , when
an entire disk fails, the RAID tries to reconstruct the disk (say , onto a
hot spare) by reading through all of the other disks in the parity g roup
and recomputing the missing values. If, during reconstruction , an LSE
is encountered on any one of the other disks, we have a problem: the
reconstruction cannot successfully complete.
To combat this issue, some systems add an extra degree of redundancy .
For example, NetApp’s RAID-DP has the equivalent of two parity disks
instead of one [C+04]. When an LSE is discovered during reconstruc tion,
the extra parity helps to reconstruct the missing block. As alw ays, there is
a cost, in that maintaining two parity blocks for each stripe is m ore costly;
however, the log-structured nature of the NetApp WAFL ﬁle system mit-
igates that cost in many cases [HLM94]. The remaining cost is sp ace, in
the form of an extra disk for the second parity block.
45.3 Detecting Corruption: The Checksum
Let’s now tackle the more challenging problem, that of silent fail ures
via data corruption. How can we prevent users from getting bad dat a
when corruption arises, and thus leads to disks returning bad d ata?
CRUX : H OW TO PRESERVE DATA INTEGRITY DESPITE CORRUPTION
Given the silent nature of such failures, what can a storage sys tem do
to detect when corruption arises? What techniques are needed? How can
one implement them efﬁciently?
Unlike latent sector errors, detection of corruption is a key problem.
How can a client tell that a block has gone bad? Once it is known that a
particular block is bad, recovery is the same as before: you need to have
some other copy of the block around (and hopefully , one that is not cor-
rupt!). Thus, we focus here on detection techniques.
The primary mechanism used by modern storage systems to preser ve
data integrity is called the checksum. A checksum is simply the result
of a function that takes a chunk of data (say a 4KB block) as input an d
computes a function over said data, producing a small summary of th e
contents of the data (say 4 or 8 bytes). This summary is referred t o as the
checksum. The goal of such a computation is to enable a system to de tect
if data has somehow been corrupted or altered by storing the checks um
with the data and then conﬁrming upon later access that the data ’s cur-
rent checksum matches the original storage value.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DATA INTEGRITY AND PROTECTION 5
TIP : T HERE ’ S NO FREE LUNCH
There’s No Such Thing As A Free Lunch, or TNSTAAFL for short, is
an old American idiom that implies that when you are seemingly ge t-
ting something for free, in actuality you are likely paying some c ost for
it. It comes from the old days when diners would advertise a free lu nch
for customers, hoping to draw them in; only when you went in, did you
realize that to acquire the “free” lunch, you had to purchase on e or more
alcoholic beverages. Of course, this may not actually be a problem, partic-
ularly if you are an aspiring alcoholic (or typical undergraduat e student).
Common Checksum Functions
A number of different functions are used to compute checksums, a nd
vary in strength (i.e., how good they are at protecting data integ rity) and
speed (i.e., how quickly can they be computed). A trade-off that is com-
mon in systems arises here: usually , the more protection you get, t he
costlier it is. There is no such thing as a free lunch.
One simple checksum function that some use is based on exclusive
or (XOR). With XOR-based checksums, the checksum is computed b y
XOR’ing each chunk of the data block being checksummed, thus prod uc-
ing a single value that represents the XOR of the entire block.
To make this more concrete, imagine we are computing a 4-byte check-
sum over a block of 16 bytes (this block is of course too small to really be a
disk sector or block, but it will serve for the example). The 16 dat a bytes,
in hex, look like this:
365e c4cd ba14 8a92 ecef 2c3a 40be f666
If we view them in binary , we get the following:
0011 0110 0101 1110 1100 0100 1100 1101
1011 1010 0001 0100 1000 1010 1001 0010
1110 1100 1110 1111 0010 1100 0011 1010
0100 0000 1011 1110 1111 0110 0110 0110
Because we’ve lined up the data in groups of 4 bytes per row, it is ea sy
to see what the resulting checksum will be: perform an XOR over e ach
column to get the ﬁnal checksum value:
0010 0000 0001 1011 1001 0100 0000 0011
The result, in hex, is 0x201b9403.
XOR is a reasonable checksum but has its limitations. If, for exa mple,
two bits in the same position within each checksummed unit chan ge, the
checksum will not detect the corruption. For this reason, people ha ve
investigated other checksum functions.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

6 D ATA INTEGRITY AND PROTECTION
Another basic checksum function is addition. This approach has t he
advantage of being fast; computing it just requires performing2’s-complement
addition over each chunk of the data, ignoring overﬂow. It can detec t
many changes in data, but is not good if the data, for example, is sh ifted.
A slightly more complex algorithm is known as the Fletcher check-
sum, named (as you might guess) for the inventor, John G. Fletcher [F8 2].
It is quite simple to compute and involves the computation of two ch eck
bytes, s1 and s2. Speciﬁcally , assume a block D consists of bytes d1 ...
dn; s1 is deﬁned as follows: s1 = ( s1 + di) mod 255 (computed over all
di); s2 in turn is: s2 = ( s2 + s1) mod 255 (again over all di) [F04]. The
Fletcher checksum is almost as strong as the CRC (see below), det ecting
all single-bit, double-bit errors, and many burst errors [F04] .
One ﬁnal commonly-used checksum is known as a cyclic redundancy
check (CRC). Assume you wish to compute the checksum over a data
block D. All you do is treat D as if it is a large binary number (it is just
a string of bits after all) and divide it by an agreed upon value ( k). The
remainder of this division is the value of the CRC. As it turns out, one
can implement this binary modulo operation rather efﬁciently , and hence
the popularity of the CRC in networking as well. See elsewhere for m ore
details [M13].
Whatever the method used, it should be obvious that there is no per -
fect checksum: it is possible two data blocks with non-identica l contents
will have identical checksums, something referred to as a collision. This
fact should be intuitive: after all, computing a checksum is ta king some-
thing large (e.g., 4KB) and producing a summary that is much sm aller
(e.g., 4 or 8 bytes). In choosing a good checksum function, we are thu s
trying to ﬁnd one that minimizes the chance of collisions while re main-
ing easy to compute.
Checksum Layout
Now that you understand a bit about how to compute a checksum, let’s
next analyze how to use checksums in a storage system. The ﬁrst question
we must address is the layout of the checksum, i.e., how should che ck-
sums be stored on disk?
The most basic approach simply stores a checksum with each disk s ec-
tor (or block). Given a data block D, let us call the checksum over that
data C(D). Thus, without checksums, the disk layout looks like this:
D0 D1 D2 D3 D4 D5 D6
With checksums, the layout adds a single checksum for every bloc k:
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DATA INTEGRITY AND PROTECTION 7
C[D0]
D0
C[D1]
D1
C[D2]
D2
C[D3]
D3
C[D4]
D4
Because checksums are usually small (e.g., 8 bytes), and dis ks only can
write in sector-sized chunks (512 bytes) or multiples thereof, one problem
that arises is how to achieve the above layout. One solution employe d by
drive manufacturers is to format the drive with 520-byte sect ors; an extra
8 bytes per sector can be used to store the checksum.
In disks that don’t have such functionality , the ﬁle system must ﬁgure
out a way to store the checksums packed into 512-byte blocks. One such
possibility is as follows:
C[D0]
C[D1]
C[D2]
C[D3]
C[D4]
D0 D1 D2 D3 D4
In this scheme, the n checksums are stored together in a sector, fol-
lowed by n data blocks, followed by another checksum sector for the
next n blocks, and so forth. This approach has the beneﬁt of working
on all disks, but can be less efﬁcient; if the ﬁle system, for exa mple, wants
to overwrite block D1, it has to read in the checksum sector containing
C(D1), update C(D1) in it, and then write out the checksum sector and
new data block D1 (thus, one read and two writes). The earlier approach
(of one checksum per sector) just performs a single write.
45.4 Using Checksums
With a checksum layout decided upon, we can now proceed to actu-
ally understand how to use the checksums. When reading a block D, the
client (i.e., ﬁle system or storage controller) also reads its ch ecksum from
disk Cs(D), which we call the stored checksum (hence the subscript Cs).
The client then computes the checksum over the retrieved block D, which
we call the computed checksum Cc(D). At this point, the client com-
pares the stored and computed checksums; if they are equal (i.e ., Cs(D)
== Cc(D), the data has likely not been corrupted, and thus can be safely
returned to the user. If they do not match (i.e., Cs(D) != Cc(D)), this im-
plies the data has changed since the time it was stored (since t he stored
checksum reﬂects the value of the data at that time). In this ca se, we have
a corruption, which our checksum has helped us to detect.
Given a corruption, the natural question is what should we do about
it? If the storage system has a redundant copy , the answer is eas y: try to
use it instead. If the storage system has no such copy , the likel y answer is
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

8 D ATA INTEGRITY AND PROTECTION
to return an error. In either case, realize that corruption dete ction is not a
magic bullet; if there is no other way to get the non-corrupted da ta, you
are simply out of luck.
45.5 A New Problem: Misdirected Writes
The basic scheme described above works well in the general case of
corrupted blocks. However, modern disks have a couple of unusual fa il-
ure modes that require different solutions.
The ﬁrst failure mode of interest is called a misdirected write . This
arises in disk and RAID controllers which write the data to disk correctly ,
except in the wrong location. In a single-disk system, this means that the
disk wrote block Dx not to address x (as desired) but rather to address
y (thus “corrupting” Dy); in addition, within a multi-disk system, the
controller may also write Di,x not to address x of disk i but rather to
some other disk j. Thus our question:
CRUX : H OW TO HANDLE MISDIRECTED WRITES
How should a storage system or disk controller detect misdirected
writes? What additional features are required from the checks um?
The answer, not surprisingly , is simple: add a little more infor mation
to each checksum. In this case, adding a physical identiﬁer (physical ID)
is quite helpful. For example, if the stored information now contai ns the
checksum C(D) and both the disk and sector numbers of the block, it is
easy for the client to determine whether the correct information resides
within a particular locale. Speciﬁcally , if the client is read ing block 4 on
disk 10 ( D10,4), the stored information should include that disk number
and sector offset, as shown below. If the information does not match, a
misdirected write has taken place, and a corruption is now detected. Here
is an example of what this added information would look like on a two-
disk system. Note that this ﬁgure, like the others before it, is n ot to scale,
as the checksums are usually small (e.g., 8 bytes) whereas th e blocks are
much larger (e.g., 4 KB or bigger):
Disk 0
Disk 1
C[D0]
disk=0
block=0
D0
C[D1]
disk=0
block=1
D1
C[D2]
disk=0
block=2
D2
C[D0]
disk=1
block=0
D0
C[D1]
disk=1
block=1
D1
C[D2]
disk=1
block=2
D2
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DATA INTEGRITY AND PROTECTION 9
You can see from the on-disk format that there is now a fair amount of
redundancy on disk: for each block, the disk number is repeated w ithin
each block, and the offset of the block in question is also kept next to the
block itself. The presence of redundant information should be no s ur-
prise, though; redundancy is the key to error detection (in this case) and
recovery (in others). A little extra information, while not stric tly needed
with perfect disks, can go a long ways in helping detect problem atic situ-
ations should they arise.
45.6 One Last Problem: Lost Writes
Unfortunately , misdirected writes are not the last problem we w ill
address. Speciﬁcally , some modern storage devices also have an i ssue
known as a lost write , which occurs when the device informs the up-
per layer that a write has completed but in fact it never is pers isted; thus,
what remains is the old contents of the block rather than the updat ed new
contents.
The obvious question here is: do any of our checksumming strategie s
from above (e.g., basic checksums, or physical identity) help t o detect
lost writes? Unfortunately , the answer is no: the old block likely has a
matching checksum, and the physical ID used above (disk numbe r and
block offset) will also be correct. Thus our ﬁnal problem:
CRUX : H OW TO HANDLE LOST WRITES
How should a storage system or disk controller detect lost writes?
What additional features are required from the checksum?
There are a number of possible solutions that can help [K+08]. One
classic approach [BS04] is to perform a write verify or read-after-write;
by immediately reading back the data after a write, a system c an ensure
that the data indeed reached the disk surface. This approach, however, is
quite slow, doubling the number of I/Os needed to complete a write .
Some systems add a checksum elsewhere in the system to detect los t
writes. For example, Sun’s Zettabyte File System (ZFS) includes a check-
sum in each ﬁle system inode and indirect block for every block inc luded
within a ﬁle. Thus, even if the write to a data block itself is los t, the check-
sum within the inode will not match the old data. Only if the write s to
both the inode and the data are lost simultaneously will such a sch eme
fail, an unlikely (but unfortunately , possible!) situation.
45.7 Scrubbing
Given all of this discussion, you might be wondering: when do thes e
checksums actually get checked? Of course, some amount of checki ng
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

10 D ATA INTEGRITY AND PROTECTION
occurs when data is accessed by applications, but most data is ra rely
accessed, and thus would remain unchecked. Unchecked data is prob-
lematic for a reliable storage system, as bit rot could eventuall y affect all
copies of a particular piece of data.
To remedy this problem, many systems utilize disk scrubbing of var-
ious forms [K+08]. By periodically reading through every block of the
system, and checking whether checksums are still valid, the disk system
can reduce the chances that all copies of a certain data item bec ome cor-
rupted. Typical systems schedule scans on a nightly or weekly b asis.
45.8 Overheads Of Checksumming
Before closing, we now discuss some of the overheads of using check-
sums for data protection. There are two distinct kinds of overhead s, as is
common in computer systems: space and time.
Space overheads come in two forms. The ﬁrst is on the disk (or other
storage medium) itself; each stored checksum takes up room on the d isk,
which can no longer be used for user data. A typical ratio might b e an 8-
byte checksum per 4 KB data block, for a 0.19% on-disk space overhe ad.
The second type of space overhead comes in the memory of the sys-
tem. When accessing data, there must now be room in memory for the
checksums as well as the data itself. However, if the system simply checks
the checksum and then discards it once done, this overhead is shor t-lived
and not much of a concern. Only if checksums are kept in memory (for
an added level of protection against memory corruption [Z+13]) wil l this
small overhead be observable.
While space overheads are small, the time overheads induced bycheck-
summing can be quite noticeable. Minimally , the CPU must compu te the
checksum over each block, both when the data is stored (to determi ne the
value of the stored checksum) and when it is accessed (to compute the
checksum again and compare it against the stored checksum). On e ap-
proach to reducing CPU overheads, employed by many systems that use
checksums (including network stacks), is to combine data copyi ng and
checksumming into one streamlined activity; because the copy is needed
anyhow (e.g., to copy the data from the kernel page cache into a us er
buffer), combined copying/checksumming can be quite effecti ve.
Beyond CPU overheads, some checksumming schemes can induce ex-
tra I/O overheads, particularly when checksums are stored distinctly from
the data (thus requiring extra I/Os to access them), and for an y extra I/O
needed for background scrubbing. The former can be reduced by de sign;
the latter can be tuned and thus its impact limited, perhaps b y control-
ling when such scrubbing activity takes place. The middle of t he night,
when most (not all!) productive workers have gone to bed, may be a
good time to perform such scrubbing activity and increase the rob ustness
of the storage system.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DATA INTEGRITY AND PROTECTION 11
45.9 Summary
We have discussed data protection in modern storage systems, focu s-
ing on checksum implementation and usage. Different checksums protect
against different types of faults; as storage devices evolve, n ew failure
modes will undoubtedly arise. Perhaps such change will force th e re-
search community and industry to revisit some of these basic approaches,
or invent entirely new approaches altogether. Time will tell. O r it won’t.
Time is funny that way .
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

12 D ATA INTEGRITY AND PROTECTION
References
[B+07] “An Analysis of Latent Sector Errors in Disk Drives” by L. B airavasundaram, G. Good-
son, S. Pasupathy , J. Schindler. SIGMETRICS ’07, San Diego, CA. The ﬁrst paper to study latent
sector errors in detail. The paper also won the Kenneth C. Sevcik Outstandin g Student Paper award,
named after a brilliant researcher and wonderful guy who passed away too soon . T o show the OSTEP
authors it was possible to move from the U.S. to Canada, Ken once sang us the Canadian national
anthem, standing up in the middle of a restaurant to do so. We chose the U.S., b ut got this memory.
[B+08] “An Analysis of Data Corruption in the Storage Stack” by La kshmi N. Bairavasun-
daram, Garth R. Goodson, Bianca Schroeder, Andrea C. Arpaci-Dusseau , Remzi H. Arpaci-
Dusseau. FAST ’08, San Jose, CA, February 2008. The ﬁrst paper to truly study disk corruption in
great detail, focusing on how often such corruption occurs over three years for over 1.5 million drives.
[BS04] “Commercial Fault Tolerance: A Tale of Two Systems” by Wendy Bartlett, Lisa Spainhower.
IEEE Transactions on Dependable and Secure Computing, V ol. 1:1, Janua ry 2004. This classic
in building fault tolerant systems is an excellent overview of the state of th e art from both IBM and
T andem. Another must read for those interested in the area.
[C+04] “Row-Diagonal Parity for Double Disk Failure Correction” by P . Corbett, B. English, A.
Goel, T. Grcanac, S. Kleiman, J. Leong, S. Sankar. FAST ’04, San Jose, C A, February 2004. An
early paper on how extra redundancy helps to solve the combined full-disk-f ailure/partial-disk-failure
problem. Also a nice example of how to mix more theoretical work with practical .
[F04] “Checksums and Error Control” by Peter M. Fenwick. Copy availabl e online here:
http://www.ostep.org/Citations/checksums-03.pdf. A great simple tutorial on check-
sums, available to you for the amazing cost of free.
[F82] “An Arithmetic Checksum for Serial Transmissions” by John G. Fle tcher. IEEE Trans-
actions on Communication, V ol. 30:1, January 1982. Fletcher’s original work on his eponymous
checksum. He didn’t call it the Fletcher checksum, rather he just did n’t call it anything; later, others
named it after him. So don’t blame old Fletch for this seeming act of braggadoc io. This anecdote might
remind you of Rubik; Rubik never called it “ Rubik’s cube”; rather, he just called it “my cube.”
[HLM94] “File System Design for an NFS File Server Appliance” by Da ve Hitz, James Lau,
Michael Malcolm. USENIX Spring ’94. The pioneering paper that describes the ideas and product at
the heart of NetApp’s core. Based on this system, NetApp has grown into a multi -billion dollar storage
company. T o learn more about NetApp, read Hitz’s autobiography “How to Castrate a Bul l” (which is
the actual title, no joking). And you thought you could avoid bull castration by going i nto CS.
[K+08] “Parity Lost and Parity Regained” by Andrew Krioukov , Lakshm i N. Bairavasun-
daram, Garth R. Goodson, Kiran Srinivasan, Randy Thelen, Andrea C. Arpaci-Dusseau, Remzi
H. Arpaci-Dusseau. FAST ’08, San Jose, CA, February 2008. This work explores how different
checksum schemes work (or don’t work) in protecting data. We reveal a number of interesting ﬂaws in
current protection strategies.
[M13] “Cyclic Redundancy Checks” by unknown. Available: http://www.mathpages.com/
home/kmath458.htm. A super clear and concise description of CRCs. The internet is full of i nfor-
mation, as it turns out.
[P+05] “IRON File Systems” by V . Prabhakaran, L. Bairavasundaram, N. Agrawal, H. Gunawi,
A. Arpaci-Dusseau, R. Arpaci-Dusseau. SOSP ’05, Brighton, England. Our paper on how disks
have partial failure modes, and a detailed study of how modern ﬁle systems reac t to such failures. As it
turns out, rather poorly! We found numerous bugs, design ﬂaws, and other oddi ties in this work. Some
of this has fed back into the Linux community, thus improving ﬁle system re liability. Y ou’re welcome!
[RO91] “Design and Implementation of the Log-structured File Syste m” by Mendel Rosen-
blum and John Ousterhout. SOSP ’91, Paciﬁc Grove, CA, October 1991. So cool we cite it again.
[S90] “Implementing Fault-Tolerant Services Using The State Machine Appr oach: A Tutorial”
by Fred B. Schneider. ACM Surveys, V ol. 22, No. 4, December 1990. How to build fault tolerant
services. A must read for those building distributed systems.
[Z+13] “Zettabyte Reliability with Flexible End-to-end Data Inte grity” by Y . Zhang, D. Myers,
A. Arpaci-Dusseau, R. Arpaci-Dusseau. MSST ’13, Long Beach, Californi a, May 2013. How to
add data protection to the page cache of a system. Out of space, otherwise we would w rite something...
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DATA INTEGRITY AND PROTECTION 13
Homework (Simulation)
In this homework, you’ll use checksum.py to investigate various as-
pects of checksums.
Questions
1. First just run checksum.py with no arguments. Compute the ad-
ditive, XOR-based, and Fletcher checksums. Use -c to check your
answers.
2. Now do the same, but vary the seed ( -s) to different values.
3. Sometimes the additive and XOR-based checksums produce the
same checksum (e.g., if the data value is all zeroes). Can you pa ss
in a 4-byte data value (using the -D ﬂag, e.g., -D a,b,c,d ) that
does not contain only zeroes and leads the additive and XOR-based
checksum having the same value? In general, when does this oc-
cur? Check that you are correct with the -c ﬂag.
4. Now pass in a 4-byte value that you know will produce a different
checksum values for additive and XOR. In general, when does thi s
occur?
5. Use the simulator to compute checksums twice (once each for a di f-
ferent set of numbers). The two number strings should be differ ent
(e.g., -D a1,b1,c1,d1 the ﬁrst time and -D a2,b2,c2,d2 the
second) but should produce the same additive checksum. In gen-
eral, when will the additive checksum be the same, even though the
data values are different? Check your speciﬁc answer with the -c
ﬂag.
6. Now do the same for the XOR checksum.
7. Now let’s look at a speciﬁc set of data values. The ﬁrst is: -D
1,2,3,4. What will the different checksums (additive, XOR, Fletcher)
be for this data? Now compare it to computing these checksums
over -D 4,3,2,1 . What do you notice about these three check-
sums? How does Fletcher compare to the other two? How is Fletcher
generally “better” than something like the simple additive c heck-
sum?
8. No checksum is perfect. Given a particular input of your choosi ng,
can you ﬁnd other data values that lead to the same Fletcher chec k-
sum? When, in general, does this occur? Start with a simple data
string (e.g., -D 0,1,2,3 ) and see if you can replace one of those
numbers but end up with the same Fletcher checksum. As always ,
use -c to check your answers.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

14 D ATA INTEGRITY AND PROTECTION
Homework (Code)
In this part of the homework, you’ll write some of your own code to
implement various checksums.
Questions
1. Write a short C program (called check-xor.c) that computes an
XOR-based checksum over an input ﬁle, and prints the checksum as
output. Use a 8-bit unsigned char to store the (one byte) checksu m.
Make some test ﬁles to see if it works as expected.
2. Now write a short C program (called check-fletcher.c) that
computes the Fletcher checksum over an input ﬁle. Once again,
test your program to see if it works.
3. Now compare the performance of both: is one faster than the other?
How does performance change as the size of the input ﬁle changes?
Use internal calls to gettimeofday to time the programs. Which
should you use if you care about performance? About checking
ability?
4. Read about the 16-bit CRC and then implement it. Test it on a nu m-
ber of different inputs to ensure that it works. How is its perfor-
mance as compared to the simple XOR and Fletcher? How about
its checking ability?
5. Now build a tool ( create-csum.c) that computes a single-byte
checksum for every 4KB block of a ﬁle, and records the results in
an output ﬁle (speciﬁed on the command line). Build a related tool
(check-csum.c) that reads a ﬁle, computes the checksums over
each block, and compares the results to the stored checksums stored
in another ﬁle. If there is a problem, the program should print tha t
the ﬁle has been corrupted. Test the program by manually corrupt -
ing the ﬁle.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
