Title: file-devices.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/file-devices.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:18+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

36
I/O Devices
Before delving into the main content of this part of the book (on persis-
tence), we ﬁrst introduce the concept of an input/output (I/O) device and
show how the operating system might interact with such an entity. I/O is
quite critical to computer systems, of course; imagine a program without
any input (it produces the same result each time); now imagine a pro-
gram with no output (what was the purpose of it running?). Clearl y , for
computer systems to be interesting, both input and output are re quired.
And thus, our general problem:
CRUX : H OW TO INTEGRATE I/O I NTO SYSTEMS
How should I/O be integrated into systems? What are the general
mechanisms? How can we make them efﬁcient?
36.1 System Architecture
To begin our discussion, let’s look at a “classical” diagram of a typ ical
system (Figure 36.1, page 2). The picture shows a single CPU at tached
to the main memory of the system via some kind of memory bus or in-
terconnect. Some devices are connected to the system via a genera l I/O
bus, which in many modern systems would be PCI (or one of its many
derivatives); graphics and some other higher-performance I/O devices
might be found here. Finally , even lower down are one or more of what
we call a peripheral bus , such as SCSI, SATA, or USB. These connect
slow devices to the system, including disks, mice, and keyboards.
One question you might ask is: why do we need a hierarchical stru c-
ture like this? Put simply: physics, and cost. The faster a bus is, the
shorter it must be; thus, a high-performance memory bus does not ha ve
much room to plug devices and such into it. In addition, engineer ing
a bus for high performance is quite costly . Thus, system designe rs have
adopted this hierarchical approach, where components that demand high
performance (such as the graphics card) are nearer the CPU. Low er per-
formance components are further away . The beneﬁts of placing dis ks and
other slow devices on a peripheral bus are manifold; in particula r, you
can place a large number of devices on it.
1

2 I/O D EVICES
Graphics
MemoryCPU
Memory Bus
(proprietary)
General I/O Bus
(e.g., PCI)
Peripheral I/O Bus
(e.g., SCSI, SATA, USB)
Figure 36.1: Prototypical System Architecture
Of course, modern systems increasingly use specialized chips ets and
faster point-to-point interconnects to improve performance. Fig ure 36.2
(page 3) shows an approximate diagram of Intel’s Z270 Chipset [H1 7].
Along the top, the CPU connects most closely to the memory system,
but also has a high-performance connection to the graphics card (and
thus, the display) to enable gaming (oh, the horror!) and other gra phics-
intensive applications.
The CPU connects to an I/O chip via Intel’s proprietary DMI (Direct
Media Interface ), and the rest of the devices connect to this chip via a
number of different interconnects. On the right, one or more hard d rives
connect to the system via the eSATAinterface; ATA(the AT Attachment,
in reference to providing connection to the IBM PC AT), then SATA (for
Serial ATA), and now eSATA (for external SATA) represent an evolu-
tion of storage interfaces over the past decades, with each step f orward
increasing performance to keep pace with modern storage device s.
Below the I/O chip are a number of USB (Universal Serial Bus ) con-
nections, which in this depiction enable a keyboard and mouse to b e at-
tached to the computer. On many modern systems, USB is used for low
performance devices such as these.
Finally , on the left, other higher performance devices can be connected
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

I/O D EVICES 3
PCIe
Graphics
Memory
Interconnect
Graphics CPU Memory
DMI
I/O Chip
eSATA
Disk
Disk
Disk
Disk
USB
Keyboard
Mouse
PCIe
Network
Figure 36.2: Modern System Architecture
to the system via PCIe (Peripheral Component Interconnect Express). In
this diagram, a network interface is attached to the system he re; higher
performance storage devices (such as NVMe persistent storage devices)
are often connected here.
36.2 A Canonical Device
Let us now look at a canonical device (not a real one), and use this
device to drive our understanding of some of the machinery requir ed to
make device interaction efﬁcient. From Figure 36.3 (page 4), w e can see
that a device has two important components. The ﬁrst is the hardw are
interface it presents to the rest of the system. Just like a piece of softwar e,
hardware must also present some kind of interface that allows th e system
software to control its operation. Thus, all devices have some spec iﬁed
interface and protocol for typical interaction.
The second part of any device is its internal structure . This part of
the device is implementation speciﬁc and is responsible for imp lement-
ing the abstraction the device presents to the system. V ery simple devices
will have one or a few hardware chips to implement their function ality;
more complex devices will include a simple CPU, some general pur pose
memory , and other device-speciﬁc chips to get their job done. For e xam-
ple, modern RAID controllers might consist of hundreds of thousands of
lines of ﬁrmware (i.e., software within a hardware device) to implement
its functionality .
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

4 I/O D EVICES
Other Hardware-specific Chips
Memory (DRAM or SRAM or both)
Micro-controller (CPU)
Registers Status Command Data Interface
Internals
Figure 36.3: A Canonical Device
36.3 The Canonical Protocol
In the picture above, the (simpliﬁed) device interface is comp rised of
three registers: a status register, which can be read to see the current sta-
tus of the device; a command register, to tell the device to perform a cer-
tain task; and a data register to pass data to the device, or get data from
the device. By reading and writing these registers, the opera ting system
can control device behavior.
Let us now describe a typical interaction that the OS might have with
the device in order to get the device to do something on its behalf . The
protocol is as follows:
While (STATUS == BUSY)
; // wait until device is not busy
Write data to DATA register
Write command to COMMAND register
(starts the device and executes the command)
While (STATUS == BUSY)
; // wait until device is done with your request
The protocol has four steps. In the ﬁrst, the OS waits until the dev ice is
ready to receive a command by repeatedly reading the status re gister; we
call this polling the device (basically , just asking it what is going on). Sec-
ond, the OS sends some data down to the data register; one can imagi ne
that if this were a disk, for example, that multiple writes woul d need to
take place to transfer a disk block (say 4KB) to the device. Whe n the main
CPU is involved with the data movement (as in this example protocol ),
we refer to it as programmed I/O (PIO). Third, the OS writes a command
to the command register; doing so implicitly lets the device kn ow that
both the data is present and that it should begin working on the com-
mand. Finally , the OS waits for the device to ﬁnish by again poll ing it
in a loop, waiting to see if it is ﬁnished (it may then get an error c ode to
indicate success or failure).
This basic protocol has the positive aspect of being simple and work -
ing. However, there are some inefﬁciencies and inconveniences involved.
The ﬁrst problem you might notice in the protocol is that polling seem s
inefﬁcient; speciﬁcally , it wastes a great deal of CPU time ju st waiting for
the (potentially slow) device to complete its activity , instead of switching
to another ready process and thus better utilizing the CPU.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

I/O D EVICES 5
THE CRUX : H OW TO AVOID THE COSTS OF POLLING
How can the OS check device status without frequent polling, and
thus lower the CPU overhead required to manage the device?
36.4 Lowering CPU Overhead With Interrupts
The invention that many engineers came upon years ago to improve
this interaction is something we’ve seen already: the interrupt. Instead of
polling the device repeatedly , the OS can issue a request, put the calling
process to sleep, and context switch to another task. When the de vice
is ﬁnally ﬁnished with the operation, it will raise a hardware i nterrupt,
causing the CPU to jump into the OS at a predetermined interrupt service
routine (ISR) or more simply an interrupt handler. The handler is just a
piece of operating system code that will ﬁnish the request (for ex ample,
by reading data and perhaps an error code from the device) and wak e the
process waiting for the I/O, which can then proceed as desired.
Interrupts thus allow for overlap of computation and I/O, which is
key for improved utilization. This timeline shows the problem:
CPU
Disk 1 1 1 1 1
1 1 1 1 1 p p p p p 1 1 1 1 1
In the diagram, Process 1 runs on the CPU for some time (indicated b y
a repeated 1 on the CPU line), and then issues an I/O request to the disk
to read some data. Without interrupts, the system simply spins , polling
the status of the device repeatedly until the I/O is complete (i ndicated by
a p). The disk services the request and ﬁnally Process 1 can run ag ain.
If instead we utilize interrupts and allow for overlap, the OS ca n do
something else while waiting for the disk:
CPU
Disk 1 1 1 1 1
1 1 1 1 1 2 2 2 2 2 1 1 1 1 1
In this example, the OS runs Process 2 on the CPU while the disk se r-
vices Process 1’s request. When the disk request is ﬁnished, an interrupt
occurs, and the OS wakes up Process 1 and runs it again. Thus, both the
CPU and the disk are properly utilized during the middle stret ch of time.
Note that using interrupts is not always the best solution. For example,
imagine a device that performs its tasks very quickly: the ﬁrs t poll usually
ﬁnds the device to be done with task. Using an interrupt in this case will
actually slow down the system: switching to another process, handling the
interrupt, and switching back to the issuing process is expen sive. Thus, if
a device is fast, it may be best to poll; if it is slow, interrupts , which allow
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

6 I/O D EVICES
TIP : I NTERRUPTS NOT ALWAYS BETTER THAN POLLING
Although interrupts allow for overlap of computation and I/O, they on ly
really make sense for slow devices. Otherwise, the cost of interr upt han-
dling and context switching may outweigh the beneﬁts interrup ts pro-
vide. There are also cases where a ﬂood of interrupts may overload a sys-
tem and lead it to livelock [MR96]; in such cases, polling provid es more
control to the OS in its scheduling and thus is again useful.
overlap, are best. If the speed of the device is not known, or sometim es
fast and sometimes slow, it may be best to use a hybrid that polls for a
little while and then, if the device is not yet ﬁnished, uses in terrupts. This
two-phased approach may achieve the best of both worlds.
Another reason not to use interrupts arises in networks [MR96]. W hen
a huge stream of incoming packets each generate an interrupt, i t is pos-
sible for the OS to livelock, that is, ﬁnd itself only processing interrupts
and never allowing a user-level process to run and actually ser vice the re-
quests. For example, imagine a web server that experiences a l oad burst
because it became the top-ranked entry on hacker news [H18]. In this
case, it is better to occasionally use polling to better control wh at is hap-
pening in the system and allow the web server to service some req uests
before going back to the device to check for more packet arrivals.
Another interrupt-based optimization is coalescing. In such a setup, a
device which needs to raise an interrupt ﬁrst waits for a bit be fore deliv-
ering the interrupt to the CPU. While waiting, other requests may soon
complete, and thus multiple interrupts can be coalesced into a single in-
terrupt delivery , thus lowering the overhead of interrupt proce ssing. Of
course, waiting too long will increase the latency of a request, a common
trade-off in systems. See Ahmad et al. [A+11] for an excellent su mmary .
36.5 More Efﬁcient Data Movement With DMA
Unfortunately , there is one other aspect of our canonical protocol tha t
requires our attention. In particular, when using programmed I /O (PIO)
to transfer a large chunk of data to a device, the CPU is once agai n over-
burdened with a rather trivial task, and thus wastes a lot of tim e and
effort that could better be spent running other processes. This t imeline
illustrates the problem:
CPU
Disk 1 1 1 1 1
1 1 1 1 1 c c c 2 2 2 2 2 1 1
In the timeline, Process 1 is running and then wishes to write some data to
the disk. It then initiates the I/O, which must copy the data fr om memory
to the device explicitly , one word at a time (marked c in the diagram).
When the copy is complete, the I/O begins on the disk and the CPU ca n
ﬁnally be used for something else.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

I/O D EVICES 7
THE CRUX : H OW TO LOWER PIO O VERHEADS
With PIO, the CPU spends too much time moving data to and from
devices by hand. How can we ofﬂoad this work and thus allow the CPU
to be more effectively utilized?
The solution to this problem is something we refer to as Direct Mem-
ory Access (DMA) . A DMA engine is essentially a very speciﬁc device
within a system that can orchestrate transfers between devic es and main
memory without much CPU intervention.
DMA works as follows. To transfer data to the device, for example, the
OS would program the DMA engine by telling it where the data live s in
memory , how much data to copy , and which device to send it to. At tha t
point, the OS is done with the transfer and can proceed with other w ork.
When the DMA is complete, the DMA controller raises an interrupt , and
the OS thus knows the transfer is complete. The revised timelin e:
CPU
DMA
Disk 1 1 1 1 1
1 1 1 1 1 2 2 2 2 2 2 2 2 1 1
c c c
From the timeline, you can see that the copying of data is now handled
by the DMA controller. Because the CPU is free during that time, the OS
can do something else, here choosing to run Process 2. Process 2 thu s gets
to use more CPU before Process 1 runs again.
36.6 Methods Of Device Interaction
Now that we have some sense of the efﬁciency issues involved with
performing I/O, there are a few other problems we need to handle t o
incorporate devices into modern systems. One problem you may have
noticed thus far: we have not really said anything about how the OS ac-
tually communicates with the device! Thus, the problem:
THE CRUX : H OW TO COMMUNICATE WITH DEVICES
How should the hardware communicate with a device? Should there
be explicit instructions? Or are there other ways to do it?
Over time, two primary methods of device communication have de-
veloped. The ﬁrst, oldest method (used by IBM mainframes for many
years) is to have explicit I/O instructions . These instructions specify a
way for the OS to send data to speciﬁc device registers and thus allow the
construction of the protocols described above.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

8 I/O D EVICES
For example, on x86, the in and out instructions can be used to com-
municate with devices. For example, to send data to a device, t he caller
speciﬁes a register with the data in it, and a speciﬁc port which names the
device. Executing the instruction leads to the desired behav ior.
Such instructions are usually privileged. The OS controls devices, and
the OS thus is the only entity allowed to directly communicate with them.
Imagine if any program could read or write the disk, for example: t otal
chaos (as always), as any user program could use such a loophole to ga in
complete control over the machine.
The second method to interact with devices is known as memory-
mapped I/O . With this approach, the hardware makes device registers
available as if they were memory locations. To access a particular register,
the OS issues a load (to read) or store (to write) the address; the hardware
then routes the load/store to the device instead of main memory .
There is not some great advantage to one approach or the other. The
memory-mapped approach is nice in that no new instructions are n eeded
to support it, but both approaches are still in use today .
36.7 Fitting Into The OS: The Device Driver
One ﬁnal problem we will discuss: how to ﬁt devices, each of which
have very speciﬁc interfaces, into the OS, which we would like t o keep
as general as possible. For example, consider a ﬁle system. We’d l ike
to build a ﬁle system that worked on top of SCSI disks, IDE disks, USB
keychain drives, and so forth, and we’d like the ﬁle system to be relatively
oblivious to all of the details of how to issue a read or write request to
these different types of drives. Thus, our problem:
THE CRUX : H OW TO BUILD A D EVICE -NEUTRAL OS
How can we keep most of the OS device-neutral, thus hiding the de-
tails of device interactions from major OS subsystems?
The problem is solved through the age-old technique of abstraction.
At the lowest level, a piece of software in the OS must know in detai l
how a device works. We call this piece of software a device driver , and
any speciﬁcs of device interaction are encapsulated within.
Let us see how this abstraction might help OS design and impleme n-
tation by examining the Linux ﬁle system software stack. Figur e 36.4 is
a rough and approximate depiction of the Linux software organizati on.
As you can see from the diagram, a ﬁle system (and certainly , an a ppli-
cation above) is completely oblivious to the speciﬁcs of which disk class
it is using; it simply issues block read and write requests to t he generic
block layer, which routes them to the appropriate device driver , which
handles the details of issuing the speciﬁc request. Although s impliﬁed,
the diagram shows how such detail can be hidden from most of the OS.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

I/O D EVICES 9
Application
File System Raw
Generic Block Layer
Device Driver [SCSI, ATA, etc.]
POSIX API [open, read, write, close, etc.]
Generic Block Interface [block read/write]
Specific Block Interface [protocol-specific read/write]
user kernel mode
Figure 36.4: The File System Stack
The diagram also shows a raw interface to devices, which enables spe-
cial applications (such as a ﬁle-system checker , described later [AD14],
or a disk defragmentation tool) to directly read and write blocks without
using the ﬁle abstraction. Most systems provide this type of inte rface to
support these low-level storage management applications.
Note that the encapsulation seen above can have its downside as we ll.
For example, if there is a device that has many special capabil ities, but
has to present a generic interface to the rest of the kernel, th ose special
capabilities will go unused. This situation arises, for examp le, in Linux
with SCSI devices, which have very rich error reporting; because other
block devices (e.g., ATA/IDE) have much simpler error handlin g, all that
higher levels of software ever receive is a generic EIO (generic IO error)
error code; any extra detail that SCSI may have provided is thus lost to
the ﬁle system [G08].
Interestingly , because device drivers are needed for any dev ice you
might plug into your system, over time they have come to represen t a
huge percentage of kernel code. Studies of the Linux kernel revea l that
over 70% of OS code is found in device drivers [C01]; for Windows-bas ed
systems, it is likely quite high as well. Thus, when people tel l you that the
OS has millions of lines of code, what they are really saying is tha t the OS
has millions of lines of device-driver code. Of course, for any give n in-
stallation, most of that code may not be active (i.e., only a few devi ces are
connected to the system at a time). Perhaps more depressingly , as drivers
are often written by “amateurs” (instead of full-time kernel d evelopers),
they tend to have many more bugs and thus are a primary contribut or to
kernel crashes [S03].
36.8 Case Study: A Simple IDE Disk Driver
To dig a little deeper here, let’s take a quick look at an actual de vice: an
IDE disk drive [L94]. We summarize the protocol as described in t his ref-
erence [W10]; we’ll also peek at the xv6 source code for a simple ex ample
of a working IDE driver [CK+08].
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

10 I/O D EVICES
Control Register:
Address 0x3F6 = 0x08 (0000 1RE0): R=reset,
E=0 means "enable interrupt"
Command Block Registers:
Address 0x1F0 = Data Port
Address 0x1F1 = Error
Address 0x1F2 = Sector Count
Address 0x1F3 = LBA low byte
Address 0x1F4 = LBA mid byte
Address 0x1F5 = LBA hi byte
Address 0x1F6 = 1B1D TOP4LBA: B=LBA, D=drive
Address 0x1F7 = Command/status
Status Register (Address 0x1F7):
7 6 5 4 3 2 1 0
BUSY READY FAULT SEEK DRQ CORR IDDEX ERROR
Error Register (Address 0x1F1): (check when ERROR==1)
7 6 5 4 3 2 1 0
BBK UNC MC IDNF MCR ABRT T0NF AMNF
BBK = Bad Block
UNC = Uncorrectable data error
MC = Media Changed
IDNF = ID mark Not Found
MCR = Media Change Requested
ABRT = Command aborted
T0NF = Track 0 Not Found
AMNF = Address Mark Not Found
Figure 36.5: The IDE Interface
An IDE disk presents a simple interface to the system, consist ing of
four types of register: control, command block, status, and error. T hese
registers are available by reading or writing to speciﬁc “I/O addresses”
(such as 0x3F6 below) using (on x86) the in and out I/O instructions.
The basic protocol to interact with the device is as follows, assum ing
it has already been initialized.
• Wait for drive to be ready. Read Status Register (0x1F7) until drive
is READY and not BUSY .
• Write parameters to command registers. Write the sector count,
logical block address (LBA) of the sectors to be accessed, and dri ve
number (master=0x00 or slave=0x10, as IDE permits just two drives)
to command registers (0x1F2-0x1F6).
• Start the I/O. Write READ|WRITE command to command register
(0x1F7).
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

I/O D EVICES 11
• Data transfer (for writes): Wait until drive status is READY and
DRQ (drive request for data); write data to data port.
• Handle interrupts. In the simplest case, handle an interrupt for
each sector transferred; more complex approaches allow batching
and thus one ﬁnal interrupt when the entire transfer is complet e.
• Error handling. After each operation, read the status register. If the
ERROR bit is on, read the error register for details.
Most of this protocol is found in the xv6 IDE driver (Figure 36.6),
which (after initialization) works through four primary functi ons. The
ﬁrst is ide_rw(), which queues a request (if there are others pending),
or issues it directly to the disk (via ide_start_request()); in either
case, the routine waits for the request to complete and the calli ng process
is put to sleep. The second is ide_start_request(), which is used
to send a request (and perhaps data, in the case of a write) to th e disk;
the in and out x86 instructions are called to read and write device regis-
ters, respectively . The start request routine uses the thirdfunction, ide_-
wait_ready(), to ensure the drive is ready before issuing a request to it.
Finally ,ide_intr() is invoked when an interrupt takes place; it reads
data from the device (if the request is a read, not a write), wake s the pro-
cess waiting for the I/O to complete, and (if there are more reque sts in
the I/O queue), launches the next I/O via ide_start_request().
36.9 Historical Notes
Before ending, we include a brief historical note on the origin of som e
of these fundamental ideas. If you are interested in learning m ore, read
Smotherman’s excellent summary [S08].
Interrupts are an ancient idea, existing on the earliest of mac hines. For
example, the UNIV AC in the early 1950’s had some form of interrupt vec-
toring, although it is unclear in exactly which year this featu re was avail-
able [S08]. Sadly , even in its infancy , we are beginning to lose t he origins
of computing history .
There is also some debate as to which machine ﬁrst introduced th e idea
of DMA. For example, Knuth and others point to the DYSEAC (a “mo-
bile” machine, which at the time meant it could be hauled in a tr ailer),
whereas others think the IBM SAGE may have been the ﬁrst [S08]. Ei -
ther way , by the mid 50’s, systems with I/O devices that communi cated
directly with memory and interrupted the CPU when ﬁnished exi sted.
The history here is difﬁcult to trace because the inventions ar e tied to
real, and sometimes obscure, machines. For example, some think t hat the
Lincoln Labs TX-2 machine was ﬁrst with vectored interrupts [S0 8], but
this is hardly clear.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

12 I/O D EVICES
static int ide_wait_ready() {
while (((int r = inb(0x1f7)) & IDE_BSY) || !(r & IDE_DRDY))
; // loop until drive isn’t busy
// return -1 on error, or 0 otherwise
}
static void ide_start_request(struct buf *b) {
ide_wait_ready();
outb(0x3f6, 0); // generate interrupt
outb(0x1f2, 1); // how many sectors?
outb(0x1f3, b->sector & 0xff); // LBA goes here ...
outb(0x1f4, (b->sector >> 8) & 0xff); // ... and here
outb(0x1f5, (b->sector >> 16) & 0xff); // ... and here!
outb(0x1f6, 0xe0 | ((b->dev&1)<<4) | ((b->sector>>24)&0x 0f));
if(b->flags & B_DIRTY){
outb(0x1f7, IDE_CMD_WRITE); // this is a WRITE
outsl(0x1f0, b->data, 512/4); // transfer data too!
} else {
outb(0x1f7, IDE_CMD_READ); // this is a READ (no data)
}
}
void ide_rw(struct buf *b) {
acquire(&ide_lock);
for (struct buf **pp = &ide_queue; *pp; pp=&( *pp)->qnext)
; // walk queue
*pp = b; // add request to end
if (ide_queue == b) // if q is empty
ide_start_request(b); // send req to disk
while ((b->flags & (B_VALID|B_DIRTY)) != B_VALID)
sleep(b, &ide_lock); // wait for completion
release(&ide_lock);
}
void ide_intr() {
acquire(&ide_lock);
struct buf *b = ide_queue;
if (!(b->flags & B_DIRTY) && ide_wait_ready() >= 0)
insl(0x1f0, b->data, 512/4); // if READ: get data
b->flags |= B_VALID;
b->flags &= ˜B_DIRTY;
wakeup(b); // wake waiting process
if ((ide_queue = b->qnext) != 0) // start next request
ide_start_request(ide_queue); // (if one exists)
release(&ide_lock);
}
Figure 36.6: The xv6 IDE Disk Driver (Simpliﬁed)
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

I/O D EVICES 13
Because the ideas are relatively obvious — no Einsteinian leap is re-
quired to come up with the idea of letting the CPU do something els e
while a slow I/O is pending — perhaps our focus on “who ﬁrst?” is mis -
guided. What is certainly clear: as people built these early m achines, it
became obvious that I/O support was needed. Interrupts, DMA, an d re-
lated ideas are all direct outcomes of the nature of fast CPUs and s low
devices; if you were there at the time, you might have had simila r ideas.
36.10 Summary
You should now have a very basic understanding of how an OS inter-
acts with a device. Two techniques, the interrupt and DMA, ha ve been
introduced to help with device efﬁciency , and two approaches t o access-
ing device registers, explicit I/O instructions and memory-m apped I/O,
have been described. Finally , the notion of a device driver has b een pre-
sented, showing how the OS itself can encapsulate low-level det ails and
thus make it easier to build the rest of the OS in a device-neutr al fashion.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

14 I/O D EVICES
References
[A+11] “vIC: Interrupt Coalescing for Virtual Machine Storage Device I O” by Irfan Ahmad,
Ajay Gulati, Ali Mashtizadeh. USENIX ’11. A terriﬁc survey of interrupt coalescing in traditional
and virtualized environments.
[AD14] “Operating Systems: Three Easy Pieces” (Chapters: Crash Consis tency: FSCK and
Journaling and Log-Structured File Systems) by Remzi Arpaci-Dussea u and Andrea Arpaci-
Dusseau. Arpaci-Dusseau Books, 2014. A description of a ﬁle-system checker and how it works,
which requires low-level access to disk devices not normally provide d by the ﬁle system directly.
[C01] “An Empirical Study of Operating System Errors” by Andy Chou, Junfeng Yang, Ben-
jamin Chelf, Seth Hallem, Dawson Engler. SOSP ’01. One of the ﬁrst papers to systematically
explore how many bugs are in modern operating systems. Among other neat ﬁndi ngs, the authors show
that device drivers have something like seven times more bugs than mainli ne kernel code.
[CK+08] “The xv6 Operating System” by Russ Cox, Frans Kaashoek, Robe rt Morris, Nickolai
Zeldovich. From: http://pdos.csail.mit.edu/6.828/2008/inde x.html. See ide.c for the IDE
device driver, with a few more details therein.
[D07] “What Every Programmer Should Know About Memory” by Ulrich Dre pper. Novem-
ber, 2007. Available: http://www.akkadia.org/drepper/cpumemory.pdf. A fantastic
read about modern memory systems, starting at DRAM and going all the way up to vir tualization and
cache-optimized algorithms.
[G08] “EIO: Error-handling is Occasionally Correct” by Haryadi Gunawi, C indy Rubio-Gonzalez,
Andrea Arpaci-Dusseau, Remzi Arpaci-Dusseau, Ben Liblit. FAST ’ 08, San Jose, CA, February
2008. Our own work on building a tool to ﬁnd code in Linux ﬁle systems that does not han dle error
return properly. We found hundreds and hundreds of bugs, many of whic h have now been ﬁxed.
[H17] “Intel Core i7-7700K review: Kaby Lake Debuts for Desktop” by Joel Hruska. January 3,
2017. www.extremetech.com/extreme/241950-intels-core-i7-7700k-reviewed-kaby
-lake-debuts-desktop. An in-depth review of a recent Intel chipset, including CPUs and the
I/O subsystem.
[H18] “Hacker News” by Many contributors. Available: https://news. ycombinator.com. One
of the better aggregators for tech-related stuff. Once back in 2014, this book bec ame a highly-ranked
entry, leading to 1 million chapter downloads in just one day! Sadly, we have yet to re-experience such
a high.
[L94] “AT Attachment Interface for Disk Drives” by Lawrence J. Lamers. Re ference number:
ANSI X3.221, 1994. Available: ftp://ftp.t10.org/t13/project/d0791r4c-ATA-1.pdf.
A rather dry document about device interfaces. Read it at your own peril.
[MR96] “Eliminating Receive Livelock in an Interrupt-driven Kernel” by Jeffrey Mogul, K. K.
Ramakrishnan. USENIX ’96, San Diego, CA, January 1996. Mogul and colleagues did a great deal
of pioneering work on web server network performance. This paper is but one example.
[S08] “Interrupts” by Mark Smotherman. July ’08. Available: http://people.cs.clemson.edu/
˜mark/interrupts.html. A treasure trove of information on the history of interrupts, DMA, and
related early ideas in computing.
[S03] “Improving the Reliability of Commodity Operating Systems ” by Michael M. Swift, Brian
N. Bershad, Henry M. Levy . SOSP ’03. Swift’s work revived interest in a more microkernel-like
approach to operating systems; minimally, it ﬁnally gave some good reasons why address-space based
protection could be useful in a modern OS.
[W10] “Hard Disk Driver” by Washington State Course Homepage. A vailable online at this
site: http://eecs.wsu.edu/˜cs460/cs560/HDdriver.html. A nice summary of a simple
IDE disk drive’s interface and how to build a device driver for it.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
