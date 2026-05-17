Title: lab-projects-xv6.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/lab-projects-xv6.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:45+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

H
Laboratory: xv6 Projects
NOTE: Projects are slowing being added to https://github.com/
remzi-arpacidusseau/ostep-projects , which includes project
descriptions and a simple testing framework. Please be sure to check
that out if interested.
This chapter presents some ideas for projects related to the xv6 kernel.
The kernel is available from MIT and is quite fun to play with; d oing
these projects also make the in-class material more directly r elevant to
the projects. These projects (except perhaps the ﬁrst couple) a re usually
done in pairs, making the hard task of staring at the kernel a lit tle easier.
H.1 Intro Project
The introduction adds a simple system call to xv6. Many variant s are
possible, including a system call to count how many system calls have
taken place (one counter per system call), or other information-ga thering
calls. Students learn about how a system call actually takes pla ce.
H.2 Processes and Scheduling
Students build a more complicated scheduler than the default rou nd
robin. Many variants are possible, including a Lottery schedul er or multi-
level feedback queue. Students learn how schedulers actually work, as
well as how a context switch takes place. A small addendum is to a lso
require students to ﬁgure out how to make processes return a proper error
code when exiting, and to be able to access that error code through the
wait() system call.
1

2 L ABORATORY : XV 6 P ROJECTS
H.3 Intro to Virtual Memory
The basic idea is to add a new system call that, given a virtual address,
returns the translated physical address (or reports that the a ddress is not
valid). This lets students see how the virtual memory system se ts up page
tables without doing too much hard work. Another variant explores h ow
to transform xv6 so that a null-pointer dereference actually g enerates a
fault.
H.4 Copy-on-write Mappings
This project adds the ability to perform a lightweight fork(), called
vfork(), to xv6. This new call doesn’t simply copy the mappings but
rather sets up copy-on-write mappings to shared pages. Upon ref erence
to such a page, the kernel must then create a real copy and updat e page
tables accordingly .
H.5 Memory mappings
An alternate virtual memory project is to add some form of memory-
mapped ﬁles. Probably the easiest thing to do is to perform a laz y page-in
of code pages from an executable; a more full-blown approach is to bu ild
an mmap() system call and all of the requisite infrastructure needed to
fault in pages from disk upon dereference.
H.6 Kernel Threads
This project explores how to add kernel threads to xv6. A clone()
system call operates much like fork but uses the same address sp ace. Stu-
dents have to ﬁgure out how to implement such a call, and thus how
to create a real kernel thread. Students also should build a lit tle thread
library on top of that, providing simple locks.
H.7 Advanced Kernel Threads
Students build a full-blown thread library on top of their kernel threads,
adding different types of locks (spin locks, locks that sleep whe n the pro-
cessor is not available) as well as condition variables. Requisi te kernel
support is added as well.
H.8 Extent-based File System
This ﬁrst ﬁle system project adds some simple features to the ba sic
ﬁle system. For ﬁles of type EXTENT, students change the inode to store
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LABORATORY : XV 6 P ROJECTS 3
extents (i.e., pointer, length pairs) instead of just pointers . Serves as a
relatively light introduction to the ﬁle system.
H.9 Fast File System
Students transform the basic xv6 ﬁle system into the Berkeley F ast File
System (FFS). Students build a new mkfs tool, introduce block groups
and a new block-allocation policy , and build the large-ﬁle excep tion. The
basics of how ﬁle systems work are understood at a deeper level.
H.10 Journaling File System
Students add a rudimentary journaling layer to xv6. For each wri te to
a ﬁle, the journaling FS batches up all dirtied blocks and writes a record of
their pending update to an on-disk log; only then are the blocks mod iﬁed
in place. Students demonstrate the correctness of their system b y intro-
ducing crash points and showing that the ﬁle system always recov ers to
a consistent state.
H.11 File System Checker
Students build a simple ﬁle system checker for the xv6 ﬁle syste m.
Students learn about what makes a ﬁle system consistent and how exactly
to check for it.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES
