Title: file-ssd.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/file-ssd.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:41+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

44
Flash-based SSDs
After decades of hard-disk drive dominance, a new form of persist ent
storage device has recently gained signiﬁcance in the world. G eneri-
cally referred to as solid-state storage , such devices have no mechani-
cal or moving parts like hard drives; rather, they are simply bu ilt out of
transistors, much like memory and processors. However, unlike ty pical
random-access memory (e.g., DRAM), such a solid-state storage device
(a.k.a., an SSD) retains information despite power loss, and thus is an
ideal candidate for use in persistent storage of data.
The technology we’ll focus on is known as ﬂash (more speciﬁcally ,
NAND-based ﬂash ), which was created by Fujio Masuoka in the 1980s
[M+14]. Flash, as we’ll see, has some unique properties. For exam ple, to
write to a given chunk of it (i.e., a ﬂash page), you ﬁrst have to erase a big-
ger chunk (i.e., a ﬂash block), which can be quite expensive. In addition,
writing too often to a page will cause it to wear out. These two properties
make construction of a ﬂash-based SSD an interesting challenge:
CRUX : H OW TO BUILD A F LASH -BASED SSD
How can we build a ﬂash-based SSD? How can we handle the expen-
sive nature of erasing? How can we build a device that lasts a long time,
given that repeated overwrite will wear the device out? Will th e march of
progress in technology ever cease? Or cease to amaze?
44.1 Storing a Single Bit
Flash chips are designed to store one or more bits in a single trans is-
tor; the level of charge trapped within the transistor is mapped to a binary
value. In a single-level cell (SLC) ﬂash, only a single bit is stored within
a transistor (i.e., 1 or 0); with a multi-level cell (MLC) ﬂash, two bits are
encoded into different levels of charge, e.g., 00, 01, 10, and 1 1 are repre-
sented by low, somewhat low, somewhat high, and high levels. Ther e is
even triple-level cell (TLC) ﬂash, which encodes 3 bits per cell. Overall,
SLC chips achieve higher performance and are more expensive.
1

2 F LASH -BASED SSD S
TIP : B E CAREFUL WITH TERMINOLOGY
You may have noticed that some terms we have used many times before
(blocks, pages) are being used within the context of a ﬂash, but i n slightly
different ways than before. New terms are not created to make you r life
harder (although they may be doing just that), but arise becaus e there is
no central authority where terminology decisions are made. What is a
block to you may be a page to someone else, and vice versa, dependin g
on the context. Your job is simple: to know the appropriate terms wit hin
each domain, and use them such that people well-versed in the di scipline
can understand what you are talking about. It’s one of those times wh ere
the only solution is simple but sometimes painful: use your memory .
Of course, there are many details as to exactly how such bit-lev el stor-
age operates, down at the level of device physics. While beyond th e scope
of this book, you can read more about it on your own [J10].
44.2 From Bits to Banks/Planes
As they say in ancient Greece, storing a single bit (or a few) does not
a storage system make. Hence, ﬂash chips are organized into banks or
planes which consist of a large number of cells.
A bank is accessed in two different sized units: blocks (sometimes
called erase blocks ), which are typically of size 128 KB or 256 KB, and
pages, which are a few KB in size (e.g., 4KB). Within each bank there are
a large number of blocks; within each block, there are a large num ber of
pages. When thinking about ﬂash, you must remember this new ter mi-
nology , which is different than the blocks we refer to in disks an d RAIDs
and the pages we refer to in virtual memory .
Figure 44.1 shows an example of a ﬂash plane with blocks and pages ;
there are three blocks, each containing four pages, in this simp le exam-
ple. We’ll see below why we distinguish between blocks and pages ; it
turns out this distinction is critical for ﬂash operations such as reading
and writing, and even more so for the overall performance of the dev ice.
The most important (and weird) thing you will learn is that to wri te to
a page within a block, you ﬁrst have to erase the entire block; thi s tricky
detail makes building a ﬂash-based SSD an interesting and worth while
challenge, and the subject of the second-half of the chapter.
0 1 2Block:
Page:
Content:
00 01 02 03 04 05 06 07 08 09 10 11
Figure 44.1: A Simple Flash Chip: Pages Within Blocks
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

FLASH -BASED SSD S 3
44.3 Basic Flash Operations
Given this ﬂash organization, there are three low-level operati ons that
a ﬂash chip supports. The read command is used to read a page from the
ﬂash; erase and program are used in tandem to write. The details:
• Read (a page) : A client of the ﬂash chip can read any page (e.g.,
2KB or 4KB), simply by specifying the read command and appro-
priate page number to the device. This operation is typically q uite
fast, 10s of microseconds or so, regardless of location on the device,
and (more or less) regardless of the location of the previous request
(quite unlike a disk). Being able to access any location uniform ly
quickly means the device is a random access device.
• Erase (a block): Before writing to a page within a ﬂash, the nature
of the device requires that you ﬁrst erase the entire block the page
lies within. Erase, importantly , destroys the contents of the bl ock
(by setting each bit to the value 1); therefore, you must be sure that
any data you care about in the block has been copied elsewhere
(to memory , or perhaps to another ﬂash block) before executing the
erase. The erase command is quite expensive, taking a few mill isec-
onds to complete. Once ﬁnished, the entire block is reset and eac h
page is ready to be programmed.
• Program (a page): Once a block has been erased, the program com-
mand can be used to change some of the 1’s within a page to 0’s,
and write the desired contents of a page to the ﬂash. Program-
ming a page is less expensive than erasing a block, but more costl y
than reading a page, usually taking around 100s of microseconds
on modern ﬂash chips.
One way to think about ﬂash chips is that each page has a state as so-
ciated with it. Pages start in an INVALID state. By erasing the block that
a page resides within, you set the state of the page (and all page s within
that block) to ERASED, which resets the content of each page in the block
but also (importantly) makes them programmable. When you progra m a
page, its state changes to VALID, meaning its contents have been set and
can be read. Reads do not affect these states (although you should only
read from pages that have been programmed). Once a page has been pro-
grammed, the only way to change its contents is to erase the enti re block
within which the page resides. Here is an example of states tra nsition
after various erase and program operations within a 4-page block:
iiii Initial: pages in block are invalid (i)
Erase() → EEEE State of pages in block set to erased (E)
Program(0) → VEEE Program page 0; state set to valid (V)
Program(0) → error Cannot re-program page after programming
Program(1) → VVEE Program page 1
Erase() → EEEE Contents erased; all pages programmable
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

4 F LASH -BASED SSD S
A Detailed Example
Because the process of writing (i.e., erasing and programming) is so un-
usual, let’s go through a detailed example to make sure it makes sense.
In this example, imagine we have the following four 8-bit pages, within
a 4-page block (both unrealistically small sizes, but useful w ithin this ex-
ample); each page is VALID as each has been previously programmed.
Page 0 Page 1 Page 2 Page 3
00011000 11001110 00000001 00111111
VALID VALID VALID VALID
Now say we wish to write to page 0, ﬁlling it with new contents. To
write any page, we must ﬁrst erase the entire block. Let’s assum e we do
so, thus leaving the block in this state:
Page 0 Page 1 Page 2 Page 3
11111111 11111111 11111111 11111111
ERASED ERASED ERASED ERASED
Good news! We could now go ahead and program page 0, for exam-
ple with the contents 00000011, overwriting the old page 0 (contents
00011000) as desired. After doing so, our block looks like this:
Page 0 Page 1 Page 2 Page 3
00000011 11111111 11111111 11111111
VALID ERASED ERASED ERASED
And now the bad news: the previous contents of pages 1, 2, and 3
are all gone! Thus, before overwriting any page within a block, we must
ﬁrst move any data we care about to another location (e.g., memory , or
elsewhere on the ﬂash). The nature of erase will have a strong imp act on
how we design ﬂash-based SSDs, as we’ll soon learn about.
Summary
To summarize, reading a page is easy: just read the page. Flas h chips
do this quite well, and quickly; in terms of performance, they of fer the
potential to greatly exceed the random read performance of modern disk
drives, which are slow due to mechanical seek and rotation costs.
Writing a page is trickier; the entire block must ﬁrst be erase d (taking
care to ﬁrst move any data we care about to another location), and th en
the desired page programmed. Not only is this expensive, but fre quent
repetitions of this program/erase cycle can lead to the biggest reliability
problem ﬂash chips have: wear out . When designing a storage system
with ﬂash, the performance and reliability of writing is a cent ral focus.
We’ll soon learn more about how modern SSDs attack these issues, deliv-
ering excellent performance and reliability despite these l imitations.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

FLASH -BASED SSD S 5
Read Program Erase
Device ( µs) ( µs) ( µs)
SLC 25 200-300 1500-2000
MLC 50 600-900 ˜3000
TLC ˜75 ˜900-1350 ˜4500
Figure 44.2: Raw Flash Performance Characteristics
44.4 Flash Performance And Reliability
Because we’re interested in building a storage device out of raw ﬂ ash
chips, it is worthwhile to understand their basic performance character-
istics. Figure 44.2 presents a rough summary of some numbers foun d in
the popular press [V12]. Therein, the author presents the basi c operation
latency of reads, programs, and erases across SLC, MLC, and TLC ﬂa sh,
which store 1, 2, and 3 bits of information per cell, respectively .
As we can see from the table, read latencies are quite good, takin g just
10s of microseconds to complete. Program latency is higher and more
variable, as low as 200 microseconds for SLC, but higher as you pack
more bits into each cell; to get good write performance, you will ha ve
to make use of multiple ﬂash chips in parallel. Finally , erase s are quite
expensive, taking a few milliseconds typically . Dealing wit h this cost is
central to modern ﬂash storage design.
Let’s now consider reliability of ﬂash chips. Unlike mechanical disks,
which can fail for a wide variety of reasons (including the grues ome and
quite physical head crash , where the drive head actually makes contact
with the recording surface), ﬂash chips are pure silicon and in that sense
have fewer reliability issues to worry about. The primary conce rn is wear
out; when a ﬂash block is erased and programmed, it slowly accrues a
little bit of extra charge. Over time, as that extra charge bui lds up, it
becomes increasingly difﬁcult to differentiate between a 0 a nd a 1. At the
point where it becomes impossible, the block becomes unusable.
The typical lifetime of a block is currently not well known. Manuf ac-
turers rate MLC-based blocks as having a 10,000 P/E (Program/E rase)
cycle lifetime; that is, each block can be erased and programme d 10,000
times before failing. SLC-based chips, because they store only a single bit
per transistor, are rated with a longer lifetime, usually 100,000 P/E cycles.
However, recent research has shown that lifetimes are much long er than
expected [BD10].
One other reliability problem within ﬂash chips is known as distur-
bance. When accessing a particular page within a ﬂash, it is possibl e that
some bits get ﬂipped in neighboring pages; such bit ﬂips are know n as
read disturbs or program disturbs , depending on whether the page is
being read or programmed, respectively .
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

6 F LASH -BASED SSD S
TIP : T HE IMPORTANCE OF BACKWARDS COMPATIBILITY
Backwards compatibility is always a concern in layered system s. By
deﬁning a stable interface between two systems, one enables i nnovation
on each side of the interface while ensuring continued interoper ability .
Such an approach has been quite successful in many domains: opera ting
systems have relatively stable APIs for applications, disks p rovide the
same block-based interface to ﬁle systems, and each layer in t he IP net-
working stack provides a ﬁxed unchanging interface to the laye r above.
Not surprisingly , there can be a downside to such rigidity , as i nterfaces
deﬁned in one generation may not be appropriate in the next. In some
cases, it may be useful to think about redesigning the entire s ystem en-
tirely . An excellent example is found in the Sun ZFS ﬁle system [ B07];
by reconsidering the interaction of ﬁle systems and RAID, the cr eators of
ZFS envisioned (and then realized) a more effective integrate d whole.
44.5 From Raw Flash to Flash-Based SSDs
Given our basic understanding of ﬂash chips, we now face our next
task: how to turn a basic set of ﬂash chips into something that looks like
a typical storage device. The standard storage interface is a s imple block-
based one, where blocks (sectors) of size 512 bytes (or larger) can be read
or written, given a block address. The task of the ﬂash-based SSD is to
provide that standard block interface atop the raw ﬂash chips in side it.
Internally , an SSD consists of some number of ﬂash chips (for persis-
tent storage). An SSD also contains some amount of volatile (i.e., non-
persistent) memory (e.g., SRAM); such memory is useful for cachi ng and
buffering of data as well as for mapping tables, which we’ll lear n about
below. Finally , an SSD contains control logic to orchestrate device op era-
tion. See Agrawal et. al for details [A+08]; a simpliﬁed block dia gram is
seen in Figure 44.3 (page 7).
One of the essential functions of this control logic is to satisfy cl ient
reads and writes, turning them into internal ﬂash operations a s need be.
The ﬂash translation layer , or FTL, provides exactly this functionality .
The FTL takes read and write requests on logical blocks (that comprise the
device interface) and turns them into low-level read, erase, and program
commands on the underlying physical blocks and physical pages (that com-
prise the actual ﬂash device). The FTL should accomplish this t ask with
the goal of delivering excellent performance and high reliabil ity .
Excellent performance, as we’ll see, can be realized through a c om-
bination of techniques. One key will be to utilize multiple ﬂas h chips
in parallel; although we won’t discuss this technique much further, suf-
ﬁce it to say that all modern SSDs use multiple chips internally t o obtain
higher performance. Another performance goal will be to reduce write
ampliﬁcation, which is deﬁned as the total write trafﬁc (in bytes) issued
to the ﬂash chips by the FTL divided by the total write trafﬁc (i n bytes) is-
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

FLASH -BASED SSD S 7
Interface Logic
Flash
Controller
Memory Flash Flash Flash
Flash Flash Flash
Figure 44.3: A Flash-based SSD: Logical Diagram
sued by the client to the SSD. As we’ll see below, naive approaches t o FTL
construction will lead to high write ampliﬁcation and low perform ance.
High reliability will be achieved through the combination of a fe w dif-
ferent approaches. One main concern, as discussed above, is wear out. If
a single block is erased and programmed too often, it will become un us-
able; as a result, the FTL should try to spread writes across the blocks of
the ﬂash as evenly as possible, ensuring that all of the blocks of t he device
wear out at roughly the same time; doing so is called wear leveling and
is an essential part of any modern FTL.
Another reliability concern is program disturbance. To minimi ze such
disturbance, FTLs will commonly program pages within an erased block
in order , from low page to high page. This sequential-programming ap-
proach minimizes disturbance and is widely utilized.
44.6 FTL Organization: A Bad Approach
The simplest organization of an FTL would be something we call di-
rect mapped . In this approach, a read to logical page N is mapped di-
rectly to a read of physical page N . A write to logical page N is more
complicated; the FTL ﬁrst has to read in the entire block that pa ge N is
contained within; it then has to erase the block; ﬁnally , the FT L programs
the old pages as well as the new one.
As you can probably guess, the direct-mapped FTL has many prob-
lems, both in terms of performance as well as reliability . The performance
problems come on each write: the device has to read in the entire b lock
(costly), erase it (quite costly), and then program it (costly). The end re-
sult is severe write ampliﬁcation (proportional to the number of p ages
in a block) and as a result, terrible write performance, even sl ower than
typical hard drives with their mechanical seeks and rotationa l delays.
Even worse is the reliability of this approach. If ﬁle system met adata
or user ﬁle data is repeatedly overwritten, the same block is era sed and
programmed, over and over, rapidly wearing it out and potentially los-
ing data. The direct mapped approach simply gives too much contr ol
over wear out to the client workload; if the workload does not spread
write load evenly across its logical blocks, the underlying phys ical blocks
containing popular data will quickly wear out. For both reliabili ty and
performance reasons, a direct-mapped FTL is a bad idea.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

8 F LASH -BASED SSD S
44.7 A Log-Structured FTL
For these reasons, most FTLs today are log structured, an idea useful
in both storage devices (as we’ll see now) and ﬁle systems above the m
(e.g., in log-structured ﬁle systems ). Upon a write to logical block N ,
the device appends the write to the next free spot in the curren tly-being-
written-to block; we call this style of writing logging. To allow for subse-
quent reads of block N , the device keeps a mapping table (in its memory ,
and persistent, in some form, on the device); this table stores th e physical
address of each logical block in the system.
Let’s go through an example to make sure we understand how the
basic log-based approach works. To the client, the device looks li ke a
typical disk, in which it can read and write 512-byte sectors ( or groups of
sectors). For simplicity , assume that the client is reading or w riting 4-KB
sized chunks. Let us further assume that the SSD contains some lar ge
number of 16-KB sized blocks, each divided into four 4-KB pages; these
parameters are unrealistic (ﬂash blocks usually consist of more pages) but
will serve our didactic purposes quite well.
Assume the client issues the following sequence of operations:
• Write(100) with contents a1
• Write(101) with contents a2
• Write(2000) with contents b1
• Write(2001) with contents b2
These logical block addresses (e.g., 100) are used by the client of the
SSD (e.g., a ﬁle system) to remember where information is located.
Internally , the device must transform these block writes into the erase
and program operations supported by the raw hardware, and somehow
record, for each logical block address, which physical page of the SSD
stores its data. Assume that all blocks of the SSD are currently not v alid,
and must be erased before any page can be programmed. Here we show
the initial state of our SSD, with all pages marked INVALID (i):
0 1 2Block:
Page:
Content:
State:
00
i
01
i
02
i
03
i
04
i
05
i
06
i
07
i
08
i
09
i
10
i
11
i
When the ﬁrst write is received by the SSD (to logical block 100), t he
FTL decides to write it to physical block 0, which contains four p hysical
pages: 0, 1, 2, and 3. Because the block is not erased, we cannot wr ite to
it yet; the device must ﬁrst issue an erase command to block 0. Doi ng so
leads to the following state:
0 1 2Block:
Page:
Content:
State:
00
E
01
E
02
E
03
E
04
i
05
i
06
i
07
i
08
i
09
i
10
i
11
i
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

FLASH -BASED SSD S 9
Block 0 is now ready to be programmed. Most SSDs will write pages
in order (i.e., low to high), reducing reliability problems rel ated to pro-
gram disturbance . The SSD then directs the write of logical block 100
into physical page 0:
0 1 2Block:
Page:
Content:
State:
00
a1
V
01
E
02
E
03
E
04
i
05
i
06
i
07
i
08
i
09
i
10
i
11
i
But what if the client wants to read logical block 100? How can it ﬁnd
where it is? The SSD must transform a read issued to logical block 10 0
into a read of physical page 0. To accommodate such functionality , when
the FTL writes logical block 100 to physical page 0, it records th is fact in
an in-memory mapping table . We will track the state of this mapping
table in the diagrams as well:
Memory
Flash
Chip
Table: 100 0
0 1 2Block:
Page:
Content:
State:
00
a1
V
01
E
02
E
03
E
04
i
05
i
06
i
07
i
08
i
09
i
10
i
11
i
Now you can see what happens when the client writes to the SSD.
The SSD ﬁnds a location for the write, usually just picking the next free
page; it then programs that page with the block’s contents, and re cords
the logical-to-physical mapping in its mapping table. Subsequ ent reads
simply use the table to translate the logical block address presented by
the client into the physical page number required to read the data.
Let’s now examine the rest of the writes in our example write strea m:
101, 2000, and 2001. After writing these blocks, the state of th e device is:
Memory
Flash
Chip
Table: 100 0 101 1 2000 2 2001 3
0 1 2Block:
Page:
Content:
State:
00
a1
V
01
a2
V
02
b1
V
03
b2
V
04
i
05
i
06
i
07
i
08
i
09
i
10
i
11
i
The log-based approach by its nature improves performance (eras es
only being required once in a while, and the costly read-modify-w rite of
the direct-mapped approach avoided altogether), and greatly e nhances
reliability . The FTL can now spread writes across all pages, pe rforming
what is called wear leveling and increasing the lifetime of the device;
we’ll discuss wear leveling further below.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

10 F LASH -BASED SSD S
ASIDE : FTL M APPING INFORMATION PERSISTENCE
You might be wondering: what happens if the device loses power? Doe s
the in-memory mapping table disappear? Clearly , such informa tion can-
not truly be lost, because otherwise the device would not function a s a
persistent storage device. An SSD must have some means of recoverin g
mapping information.
The simplest thing to do is to record some mapping information wit h
each page, in what is called an out-of-band (OOB) area. When the device
loses power and is restarted, it must reconstruct its mapping ta ble by
scanning the OOB areas and reconstructing the mapping table i n mem-
ory . This basic approach has its problems; scanning a large SSD to ﬁ nd
all necessary mapping information is slow. To overcome this limit ation,
some higher-end devices use more complex logging and checkpointing
techniques to speed up recovery; learn more about logging by read ing
chapters on crash consistency and log-structured ﬁle systems [ AD14a].
Unfortunately , this basic approach to log structuring has some d own-
sides. The ﬁrst is that overwrites of logical blocks lead to someth ing we
call garbage, i.e., old versions of data around the drive and taking up
space. The device has to periodically perform garbage collection (GC) to
ﬁnd said blocks and free space for future writes; excessive gar bage collec-
tion drives up write ampliﬁcation and lowers performance. The se cond
is high cost of in-memory mapping tables; the larger the device, the more
memory such tables need. We now discuss each in turn.
44.8 Garbage Collection
The ﬁrst cost of any log-structured approach such as this one is tha t
garbage is created, and therefore garbage collection (i.e., dead-block recla-
mation) must be performed. Let’s use our continued example to make
sense of this. Recall that logical blocks 100, 101, 2000, and 200 1 have been
written to the device.
Now, let’s assume that blocks 100 and 101 are written to again, wi th
contents c1 and c2. The writes are written to the next free pages (in this
case, physical pages 4 and 5), and the mapping table is update d accord-
ingly . Note that the device must have ﬁrst erased block 1 to make such
programming possible:
Memory
Flash
Chip
Table: 100 4 101 5 2000 2 2001 3
0 1 2Block:
Page:
Content:
State:
00
a1
V
01
a2
V
02
b1
V
03
b2
V
04
c1
V
05
c2
V
06
E
07
E
08
i
09
i
10
i
11
i
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

FLASH -BASED SSD S 11
The problem we have now should be obvious: physical pages 0 and
1, although marked VALID, have garbage in them, i.e., the old versions
of blocks 100 and 101. Because of the log-structured nature of the d e-
vice, overwrites create garbage blocks, which the device must reclaim to
provide free space for new writes to take place.
The process of ﬁnding garbage blocks (also called dead blocks ) and
reclaiming them for future use is called garbage collection , and it is an
important component of any modern SSD. The basic process is simple:
ﬁnd a block that contains one or more garbage pages, read in the live
(non-garbage) pages from that block, write out those live pages to the
log, and (ﬁnally) reclaim the entire block for use in writing.
Let’s now illustrate with an example. The device decides it wan ts to
reclaim any dead pages within block 0 above. Block 0 has two dead blocks
(pages 0 and 1) and two live blocks (pages 2 and 3, which contain b locks
2000 and 2001, respectively). To do so, the device will:
• Read live data (pages 2 and 3) from block 0
• Write live data to end of the log
• Erase block 0 (freeing it for later usage)
For the garbage collector to function, there must be enough informa -
tion within each block to enable the SSD to determine whether each page
is live or dead. One natural way to achieve this end is to store, a t some
location within each block, information about which logical blocks a re
stored within each page. The device can then use the mapping ta ble to
determine whether each page within the block holds live data or n ot.
From our example above (before the garbage collection has taken place),
block 0 held logical blocks 100, 101, 2000, 2001. By checking the mapping
table (which, before garbage collection, contained 100->4, 101->5,
2000->2, 2001->3 ), the device can readily determine whether each
of the pages within the SSD block holds live information. For example,
pages 2 and 3 are clearly still pointed to by the map; pages 0 and 1 are not
and therefore are candidates for garbage collection.
When this garbage collection process is complete in our example, t he
state of the device is:
Memory
Flash
Chip
Table: 100 4 101 5 2000 6 2001 7
0 1 2Block:
Page:
Content:
State:
00
E
01
E
02
E
03
E
04
c1
V
05
c2
V
06
b1
V
07
b2
V
08
i
09
i
10
i
11
i
As you can see, garbage collection can be expensive, requiring r eading
and rewriting of live data. The ideal candidate for reclamation is a block
that consists of only dead pages; in this case, the block can immed iately
be erased and used for new data, without expensive data migrati on.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

12 F LASH -BASED SSD S
ASIDE : A N EW STORAGE API K NOWN AS TRIM
When we think of hard drives, we usually just think of the most ba-
sic interface to read and write them: read and write (there is also usu-
ally some kind of cache ﬂush command, ensuring that writes have actu-
ally been persisted, but sometimes we omit that for simplicity) . With
log-structured SSDs, and indeed, any device that keeps a ﬂexibl e and
changing mapping of logical-to-physical blocks, a new interfac e is use-
ful, known as the trim operation.
The trim operation takes an address (and possibly a length) and s imply
informs the device that the block(s) speciﬁed by the address (a nd length)
have been deleted; the device thus no longer has to track any in forma-
tion about the given address range. For a standard hard drive, tr im isn’t
particularly useful, because the drive has a static mapping of block ad-
dresses to speciﬁc platter, track, and sector(s). For a log-str uctured SSD,
however, it is highly useful to know that a block is no longer neede d, as
the SSD can then remove this information from the FTL and later recla im
the physical space during garbage collection.
Although we sometimes think of interface and implementation as s epa-
rate entities, in this case, we see that the implementation sh apes the inter-
face. With complex mappings, knowledge of which blocks are no long er
needed makes for a more effective implementation.
To reduce GC costs, some SSDs overprovision the device [A+08]; by
adding extra ﬂash capacity , cleaning can be delayed and push ed to the
background, perhaps done at a time when the device is less busy . Adding
more capacity also increases internal bandwidth, which can b e used for
cleaning and thus not harm perceived bandwidth to the client. Many
modern drives overprovision in this manner, one key to achieving e xcel-
lent overall performance.
44.9 Mapping Table Size
The second cost of log-structuring is the potential for extremely l arge
mapping tables, with one entry for each 4-KB page of the device. W ith a
large 1-TB SSD, for example, a single 4-byte entry per 4-KB page r esults
in 1 GB of memory needed by the device, just for these mappings! Th us,
this page-level FTL scheme is impractical.
Block-Based Mapping
One approach to reduce the costs of mapping is to only keep a pointer per
block of the device, instead of per page, reducing the amount of mapping
information by a factor of Size block
Size page
. This block-level FTL is akin to having
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

FLASH -BASED SSD S 13
bigger page sizes in a virtual memory system; in that case, you u se fewer
bits for the VPN and have a larger offset in each virtual address .
Unfortunately , using a block-based mapping inside a log-based FTL
does not work very well for performance reasons. The biggest problem
arises when a “small write” occurs (i.e., one that is less than t he size of
a physical block). In this case, the FTL must read a large amount of live
data from the old block and copy it into a new one (along with the data
from the small write). This data copying increases write ampli ﬁcation
greatly and thus decreases performance.
To make this issue more clear, let’s look at an example. Assume the
client previously wrote out logical blocks 2000, 2001, 2002, and 2 003 (with
contents, a, b, c, d ), and that they are located within physical block
1 at physical pages 4, 5, 6, and 7. With per-page mappings, the transla-
tion table would have to record four mappings for these logical block s:
2000→4, 2001→5, 2002→6, 2003→7.
If, instead, we use block-level mapping, the FTL only needs to r ecord
a single address translation for all of this data. The address ma pping,
however, is slightly different than our previous examples. Spec iﬁcally ,
we think of the logical address space of the device as being choppe d into
chunks that are the size of the physical blocks within the ﬂash. Thus,
the logical block address consists of two portions: a chunk number a nd
an offset. Because we are assuming four logical blocks ﬁt within e ach
physical block, the offset portion of the logical addresses requir es 2 bits;
the remaining (most signiﬁcant) bits form the chunk number.
Logical blocks 2000, 2001, 2002, and 2003 all have the same chun k
number (500), and have different offsets (0, 1, 2, and 3, respe ctively).
Thus, with a block-level mapping, the FTL records that chunk 50 0 maps
to block 1 (starting at physical page 4), as shown in this diagra m:
Memory
Flash
Chip
Table: 500 4
0 1 2Block:
Page:
Content:
State:
00
i
01
i
02
i
03
i
04
a
V
05
b
V
06
c
V
07
d
V
08
i
09
i
10
i
11
i
In a block-based FTL, reading is easy . First, the FTL extracts the chunk
number from the logical block address presented by the client, b y taking
the topmost bits out of the address. Then, the FTL looks up the chunk-
number to physical-page mapping in the table. Finally , the FTL computes
the address of the desired ﬂash page by adding the offset from the logical
address to the physical address of the block.
For example, if the client issues a read to logical address 2002 , the de-
vice extracts the logical chunk number (500), looks up the trans lation in
the mapping table (ﬁnding 4), and adds the offset from the logica l ad-
dress (2) to the translation (4). The resulting physical-pag e address (6) is
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

14 F LASH -BASED SSD S
where the data is located; the FTL can then issue the read to tha t physical
address and obtain the desired data ( c).
But what if the client writes to logical block 2002 (with content s c’)?
In this case, the FTL must read in 2000, 2001, and 2003, and the n write
out all four logical blocks in a new location, updating the mapping t able
accordingly . Block 1 (where the data used to reside) can then be erased
and reused, as shown here.
Memory
Flash
Chip
Table: 500 8
0 1 2Block:
Page:
Content:
State:
00
i
01
i
02
i
03
i
04
E
05
E
06
E
07
E
08
a
V
09
b
V
10
c’
V
11
d
V
As you can see from this example, while block level mappings grea tly
reduce the amount of memory needed for translations, they cause si gnif-
icant performance problems when writes are smaller than the ph ysical
block size of the device; as real physical blocks can be 256KB or la rger,
such writes are likely to happen quite often. Thus, a better sol ution is
needed. Can you sense that this is the part of the chapter where w e tell
you what that solution is? Better yet, can you ﬁgure it out yourself, before
reading on?
Hybrid Mapping
To enable ﬂexible writing but also reduce mapping costs, many modern
FTLs employ a hybrid mapping technique. With this approach, the FTL
keeps a few blocks erased and directs all writes to them; these are called
log blocks . Because the FTL wants to be able to write any page to any
location within the log block without all the copying required by a p ure
block-based mapping, it keeps per-page mappings for these log blocks.
The FTL thus logically has two types of mapping table in its memory: a
small set of per-page mappings in what we’ll call the log table, and a larger
set of per-block mappings in the data table. When looking for a particular
logical block, the FTL will ﬁrst consult the log table; if the logic al block’s
location is not found there, the FTL will then consult the data tabl e to ﬁnd
its location and then access the requested data.
The key to the hybrid mapping strategy is keeping the number of log
blocks small. To keep the number of log blocks small, the FTL has to pe-
riodically examine log blocks (which have a pointer per page) and switch
them into blocks that can be pointed to by only a single block pointe r.
This switch is accomplished by one of three main techniques, bas ed on
the contents of the block [KK+02].
For example, let’s say the FTL had previously written out logical p ages
1000, 1001, 1002, and 1003, and placed them in physical block 2 (physical
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

FLASH -BASED SSD S 15
pages 8, 9, 10, 11); assume the contents of the writes to 1000, 10 01, 1002,
and 1003 are a, b, c, and d, respectively .
Memory
Flash
Chip
Log Table:
Data Table: 250 8
0 1 2Block:
Page:
Content:
State:
00
i
01
i
02
i
03
i
04
i
05
i
06
i
07
i
08
a
V
09
b
V
10
c
V
11
d
V
Now assume that the client overwrites each of these blocks (with d ata
a’, b’, c’, and d’), in the exact same order, in one of the currently avail-
able log blocks, say physical block 0 (physical pages 0, 1, 2, and 3). In this
case, the FTL will have the following state:
Memory
Flash
Chip
Log Table: 1000 0 1001 1 1002 2 1003 3
Data Table: 250 8
0 1 2Block:
Page:
Content:
State:
00
a’
V
01
b’
V
02
c’
V
03
d’
V
04
i
05
i
06
i
07
i
08
a
V
09
b
V
10
c
V
11
d
V
Because these blocks have been written exactly in the same man ner as
before, the FTL can perform what is known as a switch merge . In this
case, the log block (0) now becomes the storage location for blocks 0, 1, 2,
and 3, and is pointed to by a single block pointer; the old block (2) i s now
erased and used as a log block. In this best case, all the per-pag e pointers
required replaced by a single block pointer.
Memory
Flash
Chip
Log Table:
Data Table: 250 0
0 1 2Block:
Page:
Content:
State:
00
a’
V
01
b’
V
02
c’
V
03
d’
V
04
i
05
i
06
i
07
i
08
i
09
i
10
i
11
i
This switch merge is the best case for a hybrid FTL. Unfortunate ly ,
sometimes the FTL is not so lucky . Imagine the case where we have
the same initial conditions (logical blocks 1000 ... 1003 stored i n physi-
cal block 2) but then the client overwrites logical blocks 1000 an d 1001.
What do you think happens in this case? Why is it more challengin g
to handle? (think before looking at the result on the next page)
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

16 F LASH -BASED SSD S
Memory
Flash
Chip
Log Table: 1000 0 1001 1
Data Table: 250 8
0 1 2Block:
Page:
Content:
State:
00
a’
V
01
b’
V
02
i
03
i
04
i
05
i
06
i
07
i
08
a
V
09
b
V
10
c
V
11
d
V
To reunite the other pages of this physical block, and thus be able to re-
fer to them by only a single block pointer, the FTL performs what is called
a partial merge. In this operation, logical blocks 1002 and 1003 are read
from physical block 2, and then appended to the log. The resultin g state
of the SSD is the same as the switch merge above; however, in this cas e,
the FTL had to perform extra I/O to achieve its goals, thus incre asing
write ampliﬁcation.
The ﬁnal case encountered by the FTL known as a full merge, and re-
quires even more work. In this case, the FTL must pull together pa ges
from many other blocks to perform cleaning. For example, imagine t hat
logical blocks 0, 4, 8, and 12 are written to log block A. To switch this log
block into a block-mapped page, the FTL must ﬁrst create a data b lock
containing logical blocks 0, 1, 2, and 3, and thus the FTL must rea d 1, 2,
and 3 from elsewhere and then write out 0, 1, 2, and 3 together. Nex t, the
merge must do the same for logical block 4, ﬁnding 5, 6, and 7 and re con-
ciling them into a single physical block. The same must be done f or logi-
cal blocks 8 and 12, and then (ﬁnally), the log block A can be freed. Fre-
quent full merges, as is not surprising, can seriously harm per formance
and thus should be avoided when at all possible [GY+09].
Page Mapping Plus Caching
Given the complexity of the hybrid approach above, others have sug -
gested simpler ways to reduce the memory load of page-mapped FTL s.
Probably the simplest is just to cache only the active parts of th e FTL in
memory , thus reducing the amount of memory needed [GY+09].
This approach can work well. For example, if a given workload only
accesses a small set of pages, the translations of those pages wil l be stored
in the in-memory FTL, and performance will be excellent without high
memory cost. Of course, the approach can also perform poorly . If mem-
ory cannot contain the working set of necessary translations, each access
will minimally require an extra ﬂash read to ﬁrst bring in the missing
mapping before being able to access the data itself. Even worse , to make
room for the new mapping, the FTL might have to evict an old map-
ping, and if that mapping is dirty (i.e., not yet written to the ﬂash per-
sistently), an extra write will also be incurred. However, in many cases,
the workload will display locality , and this caching approach wi ll both
reduce memory overheads and keep performance high.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

FLASH -BASED SSD S 17
44.10 Wear Leveling
Finally , a related background activity that modern FTLs must i mple-
ment is wear leveling , as introduced above. The basic idea is simple:
because multiple erase/program cycles will wear out a ﬂash bloc k, the
FTL should try its best to spread that work across all the blocks of t he de-
vice evenly . In this manner, all blocks will wear out at roughly t he same
time, instead of a few “popular” blocks quickly becoming unusabl e.
The basic log-structuring approach does a good initial job of spreading
out write load, and garbage collection helps as well. However, sometimes
a block will be ﬁlled with long-lived data that does not get over-wr itten;
in this case, garbage collection will never reclaim the block, a nd thus it
does not receive its fair share of the write load.
To remedy this problem, the FTL must periodically read all the l ive
data out of such blocks and re-write it elsewhere, thus making th e block
available for writing again. This process of wear leveling incr eases the
write ampliﬁcation of the SSD, and thus decreases performance as e xtra
I/O is required to ensure that all blocks wear at roughly the sam e rate.
Many different algorithms exist in the literature [A+08, M+1 4]; read more
if you are interested.
44.11 SSD Performance And Cost
Before closing, let’s examine the performance and cost of modern SSDs,
to better understand how they will likely be used in persisten t storage
systems. In both cases, we’ll compare to classic hard-disk driv es (HDDs),
and highlight the biggest differences between the two.
Performance
Unlike hard disk drives, ﬂash-based SSDs have no mechanical com po-
nents, and in fact are in many ways more similar to DRAM, in that they
are “random access” devices. The biggest difference in perfor mance, as
compared to disk drives, is realized when performing random rea ds and
writes; while a typical disk drive can only perform a few hundre d ran-
dom I/Os per second, SSDs can do much better. Here, we use some data
from modern SSDs to see just how much better SSDs perform; we’re par-
ticularly interested in how well the FTLs hide the performance issues of
the raw chips.
Table 44.4 shows some performance data for three different SSDs and
one top-of-the-line hard drive; the data was taken from a few diff erent
online sources [S13, T15]. The left two columns show random I/O per-
formance, and the right two columns sequential; the ﬁrst three rows show
data for three different SSDs (from Samsung, Seagate, and Intel), a nd the
last row shows performance for a hard disk drive (or HDD), in this case
a Seagate high-end drive.
We can learn a few interesting facts from the table. First, and most
dramatic, is the difference in random I/O performance between the SSDs
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

18 F LASH -BASED SSD S
Random Sequential
Reads Writes Reads Writes
Device (MB/s) (MB/s) (MB/s) (MB/s)
Samsung 840 Pro SSD 103 287 421 384
Seagate 600 SSD 84 252 424 374
Intel SSD 335 SSD 39 222 344 354
Seagate Savvio 15K.3 HDD 2 2 223 223
Figure 44.4: SSDs And Hard Drives: Performance Comparison
and the lone hard drive. While the SSDs obtain tens or even hundreds of
MB/s in random I/Os, this “high performance” hard drive has a pe ak of
just a couple MB/s (in fact, we rounded up to get to 2 MB/s). Second, you
can see that in terms of sequential performance, there is much less of a dif-
ference; while the SSDs perform better, a hard drive is still a good choice
if sequential performance is all you need. Third, you can see that SSD ran-
dom read performance is not as good as SSD random write performance.
The reason for such unexpectedly good random-write performance is due
to the log-structured design of many SSDs, which transforms random
writes into sequential ones and improves performance. Finally , because
SSDs exhibit some performance difference between sequential an d ran-
dom I/Os, many of the techniques in chapters about how to build ﬁle
systems for hard drives are still applicable to SSDs [AD14b]; al though the
magnitude of difference between sequential and random I/Os is smaller,
there is enough of a gap to carefully consider how to design ﬁle sys tems
to reduce random I/Os.
Cost
As we saw above, the performance of SSDs greatly outstrips modern hard
drives, even when performing sequential I/O. So why haven’t SSDs c om-
pletely replaced hard drives as the storage medium of choice? Th e an-
swer is simple: cost, or more speciﬁcally , cost per unit of capacit y . Cur-
rently [A15], an SSD costs something like $150 for a 250-GB drive; s uch
an SSD costs 60 cents per GB. A typical hard drive costs roughly $50 f or
1-TB of storage, which means it costs 5 cents per GB. There is stil l more
than a 10× difference in cost between these two storage media.
These performance and cost differences dictate how large-scal e stor-
age systems are built. If performance is the main concern, SSDs ar e a
terriﬁc choice, particularly if random read performance is imp ortant. If,
on the other hand, you are assembling a large data center and wish to
store massive amounts of information, the large cost difference wi ll drive
you towards hard drives. Of course, a hybrid approach can make sen se
– some storage systems are being assembled with both SSDs and hard
drives, using a smaller number of SSDs for more popular “hot” data and
delivering high performance, while storing the rest of the “cold er” (less
used) data on hard drives to save on cost. As long as the price gap ex ists,
hard drives are here to stay .
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

FLASH -BASED SSD S 19
44.12 Summary
Flash-based SSDs are becoming a common presence in laptops, desk-
tops, and servers inside the datacenters that power the world’s e conomy .
Thus, you should probably know something about them, right?
Here’s the bad news: this chapter (like many in this book) is just the
ﬁrst step in understanding the state of the art. Some places to ge t some
more information about the raw technology include research on actua l
device performance (such as that by Chen et al. [CK+09] and Gru pp et
al. [GC+09]), issues in FTL design (including works by Agrawa l et al.
[A+08], Gupta et al. [GY+09], Huang et al. [H+14], Kim et al. [ KK+02],
Lee et al. [L+07], and Zhang et al. [Z+12]), and even distribu ted systems
comprised of ﬂash (including Gordon [CG+09] and CORFU [B+12]). And,
if we may say so, a really good overview of all the things you need to do
to extract high performance from an SSD can be found in a paper on the
“unwritten contract” [HK+17].
Don’t just read academic papers; also read about recent advance s in
the popular press (e.g., [V12]). Therein you’ll learn more pract ical (but
still useful) information, such as Samsung’s use of both TLC and SLC c ells
within the same SSD to maximize performance (SLC can buffer write s
quickly) as well as capacity (TLC can store more bits per cell). And this
is, as they say , just the tip of the iceberg. Dive in and learn mor e about
this “iceberg” of research on your own, perhaps starting with Ma e t al.’s
excellent (and recent) survey [M+14]. Be careful though; icebergs can sink
even the mightiest of ships [W15].
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

20 F LASH -BASED SSD S
ASIDE : K EY SSD T ERMS
• A ﬂash chip consists of many banks, each of which is organized into
erase blocks (sometimes just called blocks). Each block is further
subdivided into some number of pages.
• Blocks are large (128KB–2MB) and contain many pages, which ar e
relatively small (1KB–8KB).
• To read from ﬂash, issue a read command with an address and
length; this allows a client to read one or more pages.
• Writing ﬂash is more complex. First, the client must erase the en-
tire block (which deletes all information within the block). The n,
the client can program each page exactly once, thus completing the
write.
• A new trim operation is useful to tell the device when a particular
block (or range of blocks) is no longer needed.
• Flash reliability is mostly determined by wear out ; if a block is
erased and programmed too often, it will become unusable.
• A ﬂash-based solid-state storage device (SSD) behaves as if it were
a normal block-based read/write disk; by using a ﬂash translation
layer (FTL), it transforms reads and writes from a client into reads,
erases, and programs to underlying ﬂash chips.
• Most FTLs are log-structured, which reduces the cost of writing
by minimizing erase/program cycles. An in-memory translation
layer tracks where logical writes were located within the phys ical
medium.
• One key problem with log-structured FTLs is the cost of garbage
collection, which leads to write ampliﬁcation.
• Another problem is the size of the mapping table, which can be-
come quite large. Using a hybrid mapping or just caching hot
pieces of the FTL are possible remedies.
• One last problem is wear leveling ; the FTL must occasionally mi-
grate data from blocks that are mostly read in order to ensure said
blocks also receive their share of the erase/program load.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

FLASH -BASED SSD S 21
References
[A+08] “Design Tradeoffs for SSD Performance” by N. Agrawal, V . Prabhakaran, T. Wobber, J.
D. Davis, M. Manasse, R. Panigrahy . USENIX ’08, San Diego California, June 2008. An excellent
overview of what goes into SSD design.
[AD14a] “Operating Systems: Three Easy Pieces” by Chapters: Crash Consistency: FSCK and
Journaling and Log-Structured File Systems. Remzi Arpaci-Dusseau and Andrea Arpaci-Dusseau.
A lot more detail here about how logging can be used in ﬁle systems; some of the same ideas can be ap-
plied inside devices too as need be.
[AD14a] “Operating Systems: Three Easy Pieces” by Chapters: Locality and the Fast File System
and File System Implementation . Remzi Arpaci-Dusseau and Andrea Arpaci-Dusseau. These
chapters cover how to build a basic ﬁle system for a hard drive. Amazingly, some of these ideas work
perfectly well on SSDs! See if you can ﬁgure out which design techniq ues are appropriate, and which
are less needed.
[A15] “Amazon Pricing Study” by Remzi Arpaci-Dusseau. February , 2015. This is not an actual
paper, but rather one of the authors going to Amazon and looking at current prices of h ard drives and
SSDs. Y ou too can repeat this study, and see what the costs are today. Do it!
[B+12] “CORFU: A Shared Log Design for Flash Clusters” by M. Balakr ishnan, D. Malkhi, V .
Prabhakaran, T. Wobber, M. Wei, J. D. Davis. NSDI ’12, San Jose, Cali fornia, April 2012. A new
way to think about designing a high-performance replicated log for cluster s using Flash.
[BD10] “Write Endurance in Flash Drives: Measurements and Analysis” by Simona Boboila,
Peter Desnoyers. FAST ’10, San Jose, California, February 2010. A cool paper that reverse en-
gineers ﬂash-device lifetimes. Endurance sometimes far exceeds man ufacturer predictions, by up to
100×.
[B07] “ZFS: The Last Word in File Systems” by Jeff Bonwick and Bill Moor e. Available here:
http://www.ostep.org/Citations/zfs_last.pdf. Was this the last word in ﬁle sys-
tems? No, but maybe it’s close.
[CG+09] “Gordon: Using Flash Memory to Build Fast, Power-efﬁcient Clusters for Data-intensive
Applications” by Adrian M. Caulﬁeld, Laura M. Grupp, Steven Swans on. ASPLOS ’09, Wash-
ington, D.C., March 2009. Early research on assembling ﬂash into larger-scale clusters; deﬁnitel y
worth a read.
[CK+09] “Understanding Intrinsic Characteristics and System Implicat ions of Flash Memory
based Solid State Drives” by Feng Chen, David A. Koufaty , and Xiaod ong Zhang. SIGMET-
RICS/Performance ’09, Seattle, Washington, June 2009. An excellent overview of SSD performance
problems circa 2009 (though now a little dated).
[G14] “The SSD Endurance Experiment” by Geoff Gasior. The Tech Report, S eptember 19,
2014. Available: http://techreport.com/review/27062. A nice set of simple experiments
measuring performance of SSDs over time. There are many other similar stud ies; use google to ﬁnd
more.
[GC+09] “Characterizing Flash Memory: Anomalies, Observations, and Applications” by L.
M. Grupp, A. M. Caulﬁeld, J. Coburn, S. Swanson, E. Yaakobi, P . H. Sie gel, J. K. Wolf. IEEE
MICRO ’09, New York, New York, December 2009. Another excellent characterization of ﬂash
performance.
[GY+09] “DFTL: a Flash Translation Layer Employing Demand-Based S elective Caching of
Page-Level Address Mappings” by Aayush Gupta, Youngjae Kim, Bhuva n Urgaonkar. ASP-
LOS ’09, Washington, D.C., March 2009. This paper gives an excellent overview of different strategies
for cleaning within hybrid SSDs as well as a new scheme which saves map ping table space and improves
performance under many workloads.
[HK+17] “The Unwritten Contract of Solid State Drives” by Jun He, Sudarsun Kannan, Andrea
C. Arpaci-Dusseau, Remzi H. Arpaci-Dusseau. EuroSys ’17, Belgr ade, Serbia, April 2017. Our
own paper which lays out ﬁve rules clients should follow in order to get the best performance out of
modern SSDs. The rules are request scale, locality, aligned sequenti ality, grouping by death time, and
uniform lifetime. Read the paper for details!
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

22 F LASH -BASED SSD S
[H+14] “An Aggressive Worn-out Flash Block Management Scheme To Allev iate SSD Perfor-
mance Degradation” by Ping Huang, Guanying Wu, Xubin He, Weijun Xiao. EuroSys ’14,
2014. Recent work showing how to really get the most out of worn-out ﬂash blocks; neat!
[J10] “Failure Mechanisms and Models for Semiconductor Devices” by Unknown a uthor. Re-
port JEP122F, November 2010. Available on the internet at this excit ing so-called web site:
http://www.jedec.org/sites/default/files/docs/JEP122F.pdf. A highly detailed
discussion of what is going on at the device level and how such devices fai l. Only for those not faint of
heart. Or physicists. Or both.
[KK+02] “A Space-Efﬁcient Flash Translation Layer For Compact Flas h Systems” by Jesung
Kim, Jong Min Kim, Sam H. Noh, Sang Lyul Min, Yookun Cho. IEEE Transactions on Con-
sumer Electronics, V olume 48, Number 2, May 2002. One of the earliest proposals to suggest
hybrid mappings.
[L+07] “A Log Buffer-Based Flash Translation Layer by Using Fully -Associative Sector Trans-
lation. ” Sang-won Lee, Tae-Sun Chung, Dong-Ho Lee, Sangwon Park, Ha-Joo S ong. ACM
Transactions on Embedded Computing Systems, V olume 6, Number 3,July 2007 A terriﬁc paper
about how to build hybrid log/block mappings.
[M+14] “A Survey of Address Translation Technologies for Flash Memor ies” by Dongzhe Ma,
Jianhua Feng, Guoliang Li. ACM Computing Surveys, V olume 46, Numbe r 3, January 2014.
Probably the best recent survey of ﬂash and related technologies.
[S13] “The Seagate 600 and 600 Pro SSD Review” by Anand Lal Shimpi. AnandT ech, May 7,
2013. Available: http://www.anandtech.com/show/6935/seagate-600-ssd-review.
One of many SSD performance measurements available on the internet. Haven’t heard of the internet?
No problem. Just go to your web browser and type “internet” into the search tool . Y ou’ll be amazed at
what you can learn.
[T15] “Performance Charts Hard Drives” by Tom’s Hardware. January 201 5. Available here:
http://www.tomshardware.com/charts/enterprise-hdd-charts. Y et another site
with performance data, this time focusing on hard drives.
[V12] “Understanding TLC Flash” by Kristian Vatto. AnandTech, Septemb er, 2012. Available:
http://www.anandtech.com/show/5067/understanding-tlc-nand. A short descrip-
tion about TLC ﬂash and its characteristics.
[W15] “List of Ships Sunk by Icebergs” by Many authors. Available at t his location on the
“web”: http://en.wikipedia.org/wiki/List
of ships sunk by icebergs. Y es, there
is a wikipedia page about ships sunk by icebergs. It is a really boring page and basically everyone knows
the only ship the iceberg-sinking-maﬁa cares about is the Titanic.
[Z+12] “De-indirection for Flash-based SSDs with Nameless Writes” by Yiying Zhang, Leo
Prasath Arulraj, Andrea C. Arpaci-Dusseau, Remzi H. Arpaci-Dusse au. FAST ’13, San Jose,
California, February 2013. Our research on a new idea to reduce mapping table space; the key is to
re-use the pointers in the ﬁle system above to store locations of blocks, instead of add ing another level of
indirection.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

FLASH -BASED SSD S 23
Homework (Simulation)
This section introduces ssd.py, a simple SSD simulator you can use
to understand better how SSDs work. Read the README for details on
how to run the simulator. It is a long README, so boil a cup of tea (caf -
feinated likely necessary), put on your reading glasses, let t he cat curl up
on your lap 1, and get to work.
Questions
1. The homework will mostly focus on the log-structured SSD, which
is simulated with the “-T log” ﬂag. We’ll use the other types of
SSDs for comparison. First, run with ﬂags -T log -s 1 -n 10
-q. Can you ﬁgure out which operations took place? Use -c to
check your answers (or just use -C instead of -q -c ). Use different
values of -s to generate different random workloads.
2. Now just show the commands and see if you can ﬁgure out the
intermediate states of the Flash. Run with ﬂags -T log -s 2 -n
10 -C to show each command. Now, determine the state of the
Flash between each command; use -F to show the states and see if
you were right. Use different random seeds to test your burgeonin g
expertise.
3. Let’s make this problem ever so slightly more interesting by a dding
the -r 20 ﬂag. What differences does this cause in the commands?
Use -c again to check your answers.
4. Performance is determined by the number of erases, programs, and
reads (we assume here that trims are free). Run the same workloa d
again as above, but without showing any intermediate states (e. g.,
-T log -s 1 -n 10 ). Can you estimate how long this workload
will take to complete? (default erase time is 1000 microseconds ,
program time is 40, and read time is 10) Use the -S ﬂag to check
your answer. You can also change the erase, program, and read
times with the -E, -W, -R ﬂags.
5. Now, compare performance of the log-structured approach and the
(very bad) direct approach ( -T direct instead of -T log ). First,
estimate how you think the direct approach will perform, then check
your answer with the -S ﬂag. In general, how much better will the
log-structured approach perform than the direct one?
6. Let us next explore the behavior of the garbage collector. To do
so, we have to set the high ( -G) and low ( -g) watermarks appro-
priately . First, let’s observe what happens when you run a large r
workload to the log-structured SSD but without any garbage col-
lection. To do this, run with ﬂags -T log -n 1000 (the high wa-
1Now you might complain, “But I’m a dog person!” To this, we say , too b ad! Get a cat,
put it on your lap, and do the homework! How else will you learn, if y ou can’t even follow
the most basic of instructions?
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

24 F LASH -BASED SSD S
termark default is 10, so the GC won’t run in this conﬁguration).
What do you think will happen? Use -C and perhaps -F to see.
7. To turn on the garbage collector, use lower values. The high wat er-
mark (-G N ) tells the system to start collecting once N blocks have
been used; the low watermark ( -g M ) tells the system to stop col-
lecting once there are only M blocks in use. What watermark values
do you think will make for a working system? Use -C and -F to
show the commands and intermediate device states and see.
8. One other useful ﬂag is -J, which shows what the collector is doing
when it runs. Run with ﬂags -T log -n 1000 -C -J to see both
the commands and the GC behavior. What do you notice about the
GC? The ﬁnal effect of GC, of course, is performance. Use -S to
look at ﬁnal statistics; how many extra reads and writes occur due
to garbage collection? Compare this to the ideal SSD ( -T ideal );
how much extra reading, writing, and erasing is there due to th e
nature of Flash? Compare it also to the direct approach; in what
way (erases, reads, programs) is the log-structured approach s upe-
rior?
9. One last aspect to explore is workload skew . Adding skew to the
workload changes writes such that more writes occur to some smaller
fraction of the logical block space. For example, running with -K
80/20 makes 80% of the writes go to 20% of the blocks. Pick some
different skews and perform many randomly-chosen operations (e.g.,
-n 1000 ), using ﬁrst -T direct to understand the skew, and then
-T log to see the impact on a log-structured device. What do you
expect will happen? One other small skew control to explore is -k
100; by adding this ﬂag to a skewed workload, the ﬁrst 100 writes
are not skewed. The idea is to ﬁrst create a lot of data, but then onl y
update some of it. What impact might that have upon a garbage
collector?
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
