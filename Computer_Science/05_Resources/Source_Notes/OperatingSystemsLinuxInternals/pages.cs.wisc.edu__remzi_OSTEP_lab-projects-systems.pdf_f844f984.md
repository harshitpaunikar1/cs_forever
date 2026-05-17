Title: lab-projects-systems.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/lab-projects-systems.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:44+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

G
Laboratory: Systems Projects
NOTE: Projects are slowing being added to https://github.com/
remzi-arpacidusseau/ostep-projects , which includes project
descriptions and a simple testing framework. Please be sure to check
that out if interested.
This chapter presents some ideas for systems projects. We usual ly do
about six or seven projects in a 15-week semester, meaning one eve ry two
weeks or so. The ﬁrst few are usually done by a single student, and the
last few in groups of size two.
Each semester, the projects follow this same outline; however, we vary
the details to keep it interesting and make “sharing” of code across semesters
more challenging (not that anyone would do that!). We also use the M oss
tool [M94] to look for this kind of “sharing”.
As for grading, we’ve tried a number of different approaches, eac h
of which have their strengths and weaknesses. Demos are fun but time
consuming. Automated test scripts are less time intensive but require a
great deal of care to get them to carefully test interesting cor ner cases.
Check the book web page for more details on these projects; if you’d lik e
the automated test scripts, we’d be happy to share.
G.1 Intro Project
The ﬁrst project is an introduction to systems programming. Typi cal
assignments have been to write some variant of the sort utility , with
different constraints. For example, sorting text data, sorting binary data,
and other similar projects all make sense. To complete the projec t, one
must get familiar with some system calls (and their return err or codes),
use a few simple data structures, and not much else.
1

2 L ABORATORY : S YSTEMS PROJECTS
G.2 U NIX Shell
In this project, students build a variant of a U NIX shell. Students learn
about process management as well as how mysterious things like pi pes
and redirects actually work. Variants include unusual featu res, like a
redirection symbol that also compresses the output via gzip. Anot her
variant is a batch mode which allows the user to batch up a few req uests
and then execute them, perhaps using different scheduling d isciplines.
G.3 Memory-allocation Library
This project explores how a chunk of memory is managed, by building
an alternative memory-allocation library (like malloc() and free()
but with different names). The project teaches students how to use mmap()
to get a chunk of anonymous memory , and then about pointers in great
detail in order to build a simple (or perhaps, more complex) free l ist to
manage the space. Variants include: best/worst ﬁt, buddy , an d various
other allocators.
G.4 Intro to Concurrency
This project introduces concurrent programming with POSIX threa ds.
Build some simple thread-safe libraries: a list, hash table, and some more
complicated data structures are good exercises in adding locks t o real-
world code. Measure the performance of coarse-grained versus ﬁne-grained
alternatives. Variants just focus on different (and perhaps m ore complex)
data structures.
G.5 Concurrent Web Server
This project explores the use of concurrency in a real-world appli ca-
tion. Students take a simple web server (or build one) and add a thr ead
pool to it, in order to serve requests concurrently . The thread pool should
be of a ﬁxed size, and use a producer/consumer bounded buffer to pa ss
requests from a main thread to the ﬁxed pool of workers. Learn how
threads, locks, and condition variables are used to build a real server.
Variants include scheduling policies for the threads.
G.6 File System Checker
This project explores on-disk data structures and their consist ency .
Students build a simple ﬁle system checker. The debugfs tool can be
used on Linux to make real ﬁle-system images; crawl through the m and
make sure all is well. To make it more difﬁcult, also ﬁx any probl ems that
are found. Variants focus on different types of problems: pointers , link
counts, use of indirect blocks, etc.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LABORATORY : S YSTEMS PROJECTS 3
G.7 File System Defragmenter
This project explores on-disk data structures and their perform ance
implications. The project should give some particular ﬁle-syst em images
to students with known fragmentation problems; students should then
crawl through the image, and look for ﬁles that are not laid out seque n-
tially . Write out a new “defragmented” image that ﬁxes this pr oblem,
perhaps reporting some statistics.
G.8 Concurrent File Server
This project combines concurrency and ﬁle systems and even a lit tle
bit of networking and distributed systems. Students build a sim ple con-
current ﬁle server. The protocol should look something like NFS, with
lookups, reads, writes, and stats. Store ﬁles within a single dis k image
(designed as a ﬁle). Variants are manifold, with different su ggested on-
disk formats and network protocols.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

4 L ABORATORY : S YSTEMS PROJECTS
References
[M94] “Moss: A System for Detecting Software Plagiarism”
Alex Aiken
Available: http://theory .stanford.edu/˜aiken/moss/
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
