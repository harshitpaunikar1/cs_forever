Title: cpu-sched-multi.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/cpu-sched-multi.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:54:58+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

10
Multiprocessor Scheduling (Advanced)
This chapter will introduce the basics of multiprocessor scheduling .
As this topic is relatively advanced, it may be best to cover it after you
have studied the topic of concurrency in some detail (i.e., the se cond ma-
jor “easy piece” of the book).
After years of existence only in the high-end of the computing spe c-
trum, multiprocessor systems are increasingly commonplace, and have
found their way into desktop machines, laptops, and even mobile d e-
vices. The rise of the multicore processor, in which multiple CPU cores
are packed onto a single chip, is the source of this proliferation; these
chips have become popular as computer architects have had a difﬁ cult
time making a single CPU much faster without using (way) too muc h
power. And thus we all now have a few CPUs available to us, which i s a
good thing, right?
Of course, there are many difﬁculties that arise with the arri val of more
than a single CPU. A primary one is that a typical application (i.e., some C
program you wrote) only uses a single CPU; adding more CPUs does not
make that single application run faster. To remedy this proble m, you’ll
have to rewrite your application to run in parallel, perhaps using threads
(as discussed in great detail in the second piece of this book). Mu lti-
threaded applications can spread work across multiple CPUs and thus
run faster when given more CPU resources.
ASIDE : A DVANCED CHAPTERS
Advanced chapters require material from a broad swath of the book t o
truly understand, while logically ﬁtting into a section that i s earlier than
said set of prerequisite materials. For example, this chapter on multipro-
cessor scheduling makes much more sense if you’ve ﬁrst read the mi ddle
piece on concurrency; however, it logically ﬁts into the part of th e book
on virtualization (generally) and CPU scheduling (speciﬁcal ly). Thus, it
is recommended such chapters be covered out of order; in this case, after
the second piece of the book.
1

2 M ULTIPROCESSOR SCHEDULING (A DVANCED )
Memory
CPU
Cache
Figure 10.1: Single CPU With Cache
Beyond applications, a new problem that arises for the operating s ys-
tem is (not surprisingly!) that of multiprocessor scheduling . Thus far
we’ve discussed a number of principles behind single-processor schedul-
ing; how can we extend those ideas to work on multiple CPUs? What
new problems must we overcome? And thus, our problem:
CRUX : H OW TO SCHEDULE JOBS ON MULTIPLE CPU S
How should the OS schedule jobs on multiple CPUs? What new prob-
lems arise? Do the same old techniques work, or are new ideas requ ired?
10.1 Background: Multiprocessor Architecture
To understand the new issues surrounding multiprocessor sched ul-
ing, we have to understand a new and fundamental difference b etween
single-CPU hardware and multi-CPU hardware. This differen ce centers
around the use of hardware caches (e.g., Figure 10.1), and exactly how
data is shared across multiple processors. We now discuss this is sue fur-
ther, at a high level. Details are available elsewhere [CSG99 ], in particular
in an upper-level or perhaps graduate computer architecture c ourse.
In a system with a single CPU, there are a hierarchy of hardware
caches that in general help the processor run programs faster. Caches
are small, fast memories that (in general) hold copies of popular data that
is found in the main memory of the system. Main memory , in contrast,
holds all of the data, but access to this larger memory is slower. By keep-
ing frequently accessed data in a cache, the system can make t he large,
slow memory appear to be a fast one.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

MULTIPROCESSOR SCHEDULING (A DVANCED ) 3
Memory
CPU CPU
Cache Cache
Bus
Figure 10.2: Two CPUs With Caches Sharing Memory
As an example, consider a program that issues an explicit load in struc-
tion to fetch a value from memory , and a simple system with only a single
CPU; the CPU has a small cache (say 64 KB) and a large main memory .
The ﬁrst time a program issues this load, the data resides in mai n mem-
ory , and thus takes a long time to fetch (perhaps in the tens of nan osec-
onds, or even hundreds). The processor, anticipating that the data may be
reused, puts a copy of the loaded data into the CPU cache. If the pr ogram
later fetches this same data item again, the CPU ﬁrst checks f or it in the
cache; if it ﬁnds it there, the data is fetched much more quickl y (say , just
a few nanoseconds), and thus the program runs faster.
Caches are thus based on the notion of locality, of which there are
two kinds: temporal locality and spatial locality. The idea behind tem-
poral locality is that when a piece of data is accessed, it is like ly to be
accessed again in the near future; imagine variables or even i nstructions
themselves being accessed over and over again in a loop. The idea b e-
hind spatial locality is that if a program accesses a data item a t address
x, it is likely to access data items near x as well; here, think of a program
streaming through an array , or instructions being executed one a fter the
other. Because locality of these types exist in many programs, ha rdware
systems can make good guesses about which data to put in a cache an d
thus work well.
Now for the tricky part: what happens when you have multiple pro-
cessors in a single system, with a single shared main memory , as we see
in Figure 10.2?
As it turns out, caching with multiple CPUs is much more compli-
cated. Imagine, for example, that a program running on CPU 1 read s
a data item (with value D) at address A; because the data is not in the
cache on CPU 1, the system fetches it from main memory , and gets th e
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

4 M ULTIPROCESSOR SCHEDULING (A DVANCED )
value D. The program then modiﬁes the value at address A, just updat-
ing its cache with the new value D′; writing the data through all the way
to main memory is slow, so the system will (usually) do that late r. Then
assume the OS decides to stop running the program and move it to CP U
2. The program then re-reads the value at address A; there is no such
data in CPU 2’s cache, and thus the system fetches the value from main
memory , and gets the old value D instead of the correct value D′. Oops!
This general problem is called the problem of cache coherence , and
there is a vast research literature that describes many diff erent subtleties
involved with solving the problem [SHW11]. Here, we will skip all of the
nuance and make some major points; take a computer architecture c lass
(or three) to learn more.
The basic solution is provided by the hardware: by monitoring mem-
ory accesses, hardware can ensure that basically the “right t hing” hap-
pens and that the view of a single shared memory is preserved. On e way
to do this on a bus-based system (as described above) is to use an old
technique known as bus snooping [G83]; each cache pays attention to
memory updates by observing the bus that connects them to main me m-
ory . When a CPU then sees an update for a data item it holds in its ca che,
it will notice the change and either invalidate its copy (i.e., remove it
from its own cache) or update it (i.e., put the new value into its cache
too). Write-back caches, as hinted at above, make this more compli cated
(because the write to main memory isn’t visible until later), b ut you can
imagine how the basic scheme might work.
10.2 Don’t Forget Synchronization
Given that the caches do all of this work to provide coherence, do p ro-
grams (or the OS itself) have to worry about anything when they ac cess
shared data? The answer, unfortunately , is yes, and is documen ted in
great detail in the second piece of this book on the topic of concurrenc y .
While we won’t get into the details here, we’ll sketch/review som e of the
basic ideas here (assuming you’re familiar with concurrency).
When accessing (and in particular, updating) shared data it ems or
structures across CPUs, mutual exclusion primitives (such aslocks) should
likely be used to guarantee correctness (other approaches, suc h as build-
ing lock-free data structures, are complex and only used on occasion;
see the chapter on deadlock in the piece on concurrency for details ). For
example, assume we have a shared queue being accessed on multi ple
CPUs concurrently . Without locks, adding or removing elements fr om
the queue concurrently will not work as expected, even with the u nder-
lying coherence protocols; one needs locks to atomically update the data
structure to its new state.
To make this more concrete, imagine this code sequence, which is used
to remove an element from a shared linked list, as we see in Figur e 10.3.
Imagine if threads on two CPUs enter this routine at the same tim e. If
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

MULTIPROCESSOR SCHEDULING (A DVANCED ) 5
1 typedef struct __Node_t {
2 int value;
3 struct __Node_t *next;
4 } Node_t;
5
6 int List_Pop() {
7 Node_t *tmp = head; // remember old head
8 int value = head->value; // ... and its value
9 head = head->next; // advance to next
10 free(tmp); // free old head
11 return value; // return value @head
12 }
Figure 10.3: Simple List Delete Code
Thread 1 executes the ﬁrst line, it will have the current valu e of head
stored in its tmp variable; if Thread 2 then executes the ﬁrst line as well,
it also will have the same value of head stored in its own private tmp
variable ( tmp is allocated on the stack, and thus each thread will have
its own private storage for it). Thus, instead of each thread remov ing
an element from the head of the list, each thread will try to remov e the
same head element, leading to all sorts of problems (such as an at tempted
double free of the head element at Line 10, as well as potentially returning
the same data value twice).
The solution, of course, is to make such routines correct via lock-
ing. In this case, allocating a simple mutex (e.g., pthread_mutex_t
m;) and then adding a lock(&m) at the beginning of the routine and
an unlock(&m) at the end will solve the problem, ensuring that the code
will execute as desired. Unfortunately , as we will see, such an approach is
not without problems, in particular with regards to performance . Speciﬁ-
cally , as the number of CPUs grows, access to a synchronized shared data
structure becomes quite slow.
10.3 One Final Issue: Cache Afﬁnity
One ﬁnal issue arises in building a multiprocessor cache sched uler,
known as cache afﬁnity [TTG95]. This notion is simple: a process, when
run on a particular CPU, builds up a fair bit of state in the cache s (and
TLBs) of the CPU. The next time the process runs, it is often advan ta-
geous to run it on the same CPU, as it will run faster if some of its st ate
is already present in the caches on that CPU. If, instead, one ru ns a pro-
cess on a different CPU each time, the performance of the process w ill be
worse, as it will have to reload the state each time it runs (note i t will run
correctly on a different CPU thanks to the cache coherence protocol s of
the hardware). Thus, a multiprocessor scheduler should conside r cache
afﬁnity when making its scheduling decisions, perhaps prefe rring to keep
a process on the same CPU if at all possible.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

6 M ULTIPROCESSOR SCHEDULING (A DVANCED )
10.4 Single-Queue Scheduling
With this background in place, we now discuss how to build a sched -
uler for a multiprocessor system. The most basic approach is to sim ply
reuse the basic framework for single processor scheduling, by pu tting all
jobs that need to be scheduled into a single queue; we call this single-
queue multiprocessor scheduling or SQMS for short. This approach
has the advantage of simplicity; it does not require much work to t ake an
existing policy that picks the best job to run next and adapt it t o work on
more than one CPU (where it might pick the best two jobs to run, if t here
are two CPUs, for example).
However, SQMS has obvious shortcomings. The ﬁrst problem is a lack
of scalability. To ensure the scheduler works correctly on multiple CPUs,
the developers will have inserted some form of locking into the code, as
described above. Locks ensure that when SQMS code accesses the si ngle
queue (say , to ﬁnd the next job to run), the proper outcome arises.
Locks, unfortunately , can greatly reduce performance, partic ularly as
the number of CPUs in the systems grows [A90]. As contention for suc h
a single lock increases, the system spends more and more time in l ock
overhead and less time doing the work the system should be doing (not e:
it would be great to include a real measurement of this in here som eday).
The second main problem with SQMS is cache afﬁnity . For example,
let us assume we have ﬁve jobs to run ( A, B, C, D, E) and four processors.
Our scheduling queue thus looks like this:
Queue A B C D E NULL
Over time, assuming each job runs for a time slice and then anothe r
job is chosen, here is a possible job schedule across CPUs:
CPU 3
CPU 2
CPU 1
CPU 0
D C B A E
C B A E D
B A E D C
A E D C B
... (repeat) ...
... (repeat) ...
... (repeat) ...
... (repeat) ...
Because each CPU simply picks the next job to run from the globall y-
shared queue, each job ends up bouncing around from CPU to CPU, thu s
doing exactly the opposite of what would make sense from the stand-
point of cache afﬁnity .
To handle this problem, most SQMS schedulers include some kind of
afﬁnity mechanism to try to make it more likely that process wil l continue
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

MULTIPROCESSOR SCHEDULING (A DVANCED ) 7
to run on the same CPU if possible. Speciﬁcally , one might provide a fﬁn-
ity for some jobs, but move others around to balance load. For example,
imagine the same ﬁve jobs scheduled as follows:
CPU 3
CPU 2
CPU 1
CPU 0
D D D D E
C C C E C
B B E B B
A E A A A
... (repeat) ...
... (repeat) ...
... (repeat) ...
... (repeat) ...
In this arrangement, jobs A through D are not moved across proces-
sors, with only job E migrating from CPU to CPU, thus preserving afﬁn-
ity for most. You could then decide to migrate a different job the ne xt
time through, thus achieving some kind of afﬁnity fairness as we ll. Im-
plementing such a scheme, however, can be complex.
Thus, we can see the SQMS approach has its strengths and weak-
nesses. It is straightforward to implement given an existing single-CPU
scheduler, which by deﬁnition has only a single queue. However, it does
not scale well (due to synchronization overheads), and it does not r eadily
preserve cache afﬁnity .
10.5 Multi-Queue Scheduling
Because of the problems caused in single-queue schedulers, som e sys-
tems opt for multiple queues, e.g., one per CPU. We call this appr oach
multi-queue multiprocessor scheduling (or MQMS).
In MQMS, our basic scheduling framework consists of multiple schedul-
ing queues. Each queue will likely follow a particular schedul ing disci-
pline, such as round robin, though of course any algorithm can be use d.
When a job enters the system, it is placed on exactly one scheduli ng
queue, according to some heuristic (e.g., random, or picking one w ith
fewer jobs than others). Then it is scheduled essentially inde pendently ,
thus avoiding the problems of information sharing and synchroniza tion
found in the single-queue approach.
For example, assume we have a system where there are just two CP Us
(labeled CPU 0 and CPU 1), and some number of jobs enter the system :
A, B, C, and D for example. Given that each CPU has a scheduling queue
now, the OS has to decide into which queue to place each job. It mi ght do
something like this:
Q0 A C Q1 B D
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

8 M ULTIPROCESSOR SCHEDULING (A DVANCED )
Depending on the queue scheduling policy , each CPU now has two
jobs to choose from when deciding what should run. For example, with
round robin, the system might produce a schedule that looks like this:
CPU 1
CPU 0 A A C C A A C C A A C C
B B D D B B D D B B D D ...
...
MQMS has a distinct advantage over SQMS in that it should be inher -
ently more scalable. As the number of CPUs grows, so too does the num -
ber of queues, and thus lock and cache contention should not become a
central problem. In addition, MQMS intrinsically provides cac he afﬁnity;
jobs stay on the same CPU and thus reap the advantage of reusing ca ched
contents therein.
But, if you’ve been paying attention, you might see that we have a n ew
problem, which is fundamental in the multi-queue based approa ch: load
imbalance. Let’s assume we have the same set up as above (four jobs,
two CPUs), but then one of the jobs (say C) ﬁnishes. We now have the
following scheduling queues:
Q0 A Q1 B D
If we then run our round-robin policy on each queue of the system, we
will see this resulting schedule:
CPU 1
CPU 0 A A A A A A A A A A A A
B B D D B B D D B B D D ...
...
As you can see from this diagram, A gets twice as much CPU as B
and D, which is not the desired outcome. Even worse, let’s imagine that
both A and C ﬁnish, leaving just jobs B and D in the system. The two
scheduling queues, and resulting timeline, will look like thi s:
Q0 Q1 B D
CPU 0
CPU 1
B B D D B B D D B B D D ...
How terrible – CPU 0 is idle! (insert dramatic and sinister music here)
And thus our CPU usage timeline looks quite sad.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

MULTIPROCESSOR SCHEDULING (A DVANCED ) 9
So what should a poor multi-queue multiprocessor scheduler do? How
can we overcome the insidious problem of load imbalance and defeat t he
evil forces of ... the Decepticons 1? How do we stop asking questions that
are hardly relevant to this otherwise wonderful book?
CRUX : H OW TO DEAL WITH LOAD IMBALANCE
How should a multi-queue multiprocessor scheduler handle load im -
balance, so as to better achieve its desired scheduling goals ?
The obvious answer to this query is to move jobs around, a technique
which we (once again) refer to as migration. By migrating a job from one
CPU to another, true load balance can be achieved.
Let’s look at a couple of examples to add some clarity . Once again, we
have a situation where one CPU is idle and the other has some jobs.
Q0 Q1 B D
In this case, the desired migration is easy to understand: the OS should
simply move one of B or D to CPU 0. The result of this single job migra-
tion is evenly balanced load and everyone is happy .
A more tricky case arises in our earlier example, where A was left
alone on CPU 0 and B and D were alternating on CPU 1:
Q0 A Q1 B D
In this case, a single migration does not solve the problem. What
would you do in this case? The answer, alas, is continuous migrati on
of one or more jobs. One possible solution is to keep switching jobs, as
we see in the following timeline. In the ﬁgure, ﬁrst A is alone on CPU 0,
and B and D alternate on CPU 1. After a few time slices, B is moved to
compete with A on CPU 0, while D enjoys a few time slices alone on CPU
1. And thus load is balanced:
CPU 0
CPU 1
A A A A B A B A B B B B
B D B D D D D D A D A D ...
...
Of course, many other possible migration patterns exist. But now f or
the tricky part: how should the system decide to enact such a mig ration?
1Little known fact is that the home planet of Cybertron was destroyed b y bad CPU
scheduling decisions. And now let that be the ﬁrst and last reference to Trans formers in this
book, for which we sincerely apologize.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

10 M ULTIPROCESSOR SCHEDULING (A DVANCED )
One basic approach is to use a technique known as work stealing
[FLR98]. With a work-stealing approach, a (source) queue that i s low
on jobs will occasionally peek at another (target) queue, to see how full
it is. If the target queue is (notably) more full than the source q ueue, the
source will “steal” one or more jobs from the target to help balance l oad.
Of course, there is a natural tension in such an approach. If you look
around at other queues too often, you will suffer from high overhead
and have trouble scaling, which was the entire purpose of implem enting
the multiple queue scheduling in the ﬁrst place! If, on the othe r hand,
you don’t look at other queues very often, you are in danger of suffering
from severe load imbalances. Finding the right threshold remai ns, as is
common in system policy design, a black art.
10.6 Linux Multiprocessor Schedulers
Interestingly , in the Linux community , no common solution has emerged
to building a multiprocessor scheduler. Over time, three diff erent sched-
ulers arose: the O(1) scheduler, the Completely Fair Scheduler (CFS),
and the BF Scheduler (BFS) 2. See Meehean’s dissertation for an excellent
overview of the strengths and weaknesses of said schedulers [M1 1]; here
we just summarize a few of the basics.
Both O(1) and CFS use multiple queues, whereas BFS uses a singl e
queue, showing that both approaches can be successful. Of course , there
are many other details which separate these schedulers. For ex ample, the
O(1) scheduler is a priority-based scheduler (similar to the MLFQ dis-
cussed before), changing a process’s priority over time and then s chedul-
ing those with highest priority in order to meet various scheduli ng objec-
tives; interactivity is a particular focus. CFS, in contrast, i s a deterministic
proportional-share approach (more like Stride scheduling, as dis cussed
earlier). BFS, the only single-queue approach among the three, i s also
proportional-share, but based on a more complicated scheme known as
Earliest Eligible Virtual Deadline First (EEVDF) [SA96]. Re ad more about
these modern algorithms on your own; you should be able to understand
how they work now!
10.7 Summary
We have seen various approaches to multiprocessor scheduling. T he
single-queue approach (SQMS) is rather straightforward to build and bal-
ances load well but inherently has difﬁculty with scaling to m any pro-
cessors and cache afﬁnity . The multiple-queue approach (MQMS) scales
better and handles cache afﬁnity well, but has trouble with loa d imbal-
ance and is more complicated. Whichever approach you take, there is no
simple answer: building a general purpose scheduler remains a daunting
task, as small code changes can lead to large behavioral differ ences. Only
undertake such an exercise if you know exactly what you are doing, or,
at least, are getting paid a large amount of money to do so.
2Look up what BF stands for on your own; be forewarned, it is not for the faint of heart.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

MULTIPROCESSOR SCHEDULING (A DVANCED ) 11
References
[A90] “The Performance of Spin Lock Alternatives for Shared-Memory Multipr ocessors” by
Thomas E. Anderson. IEEE TPDS V olume 1:1, January 1990. A classic paper on how different
locking alternatives do and don’t scale. By T om Anderson, very well known re searcher in both systems
and networking. And author of a very ﬁne OS textbook, we must say.
[B+10] “An Analysis of Linux Scalability to Many Cores Abstract” by S ilas Boyd-Wickizer,
Austin T. Clements, Yandong Mao, Aleksey Pesterev , M. Frans Kaashoek, Robert Morris, Nick-
olai Zeldovich. OSDI ’10, Vancouver, Canada, October 2010. A terriﬁc modern paper on the
difﬁculties of scaling Linux to many cores.
[CSG99] “Parallel Computer Architecture: A Hardware/Software Ap proach” by David E.
Culler, Jaswinder Pal Singh, and Anoop Gupta. Morgan Kaufmann, 1999. A treasure ﬁlled
with details about parallel machines and algorithms. As Mark Hill humorously observes on the jacket,
the book contains more information than most research papers.
[FLR98] “The Implementation of the Cilk-5 Multithreaded Language” by Matteo Frigo, Charles
E. Leiserson, Keith Randall. PLDI ’98, Montreal, Canada, June 1998. Cilk is a lightweight
language and runtime for writing parallel programs, and an excellent examp le of the work-stealing
paradigm.
[G83] “Using Cache Memory To Reduce Processor-Memory Trafﬁc” by James R. G oodman.
ISCA ’83, Stockholm, Sweden, June 1983. The pioneering paper on how to use bus snooping, i.e.,
paying attention to requests you see on the bus, to build a cache coherence protoc ol. Goodman’s research
over many years at Wisconsin is full of cleverness, this being but one e xample.
[M11] “Towards Transparent CPU Scheduling” by Joseph T. Meehean. Doctoral Dissertation
at University of Wisconsin—Madison, 2011. A dissertation that covers a lot of the details of how
modern Linux multiprocessor scheduling works. Pretty awesome! But, as co-ad visors of Joe’s, we may
be a bit biased here.
[SHW11] “A Primer on Memory Consistency and Cache Coherence” by Daniel J. Sor in, Mark
D. Hill, and David A. Wood. Synthesis Lectures in Computer Architect ure. Morgan and Clay-
pool Publishers, May 2011. A deﬁnitive overview of memory consistency and multiprocessor caching.
Required reading for anyone who likes to know way too much about a given topic.
[SA96] “Earliest Eligible Virtual Deadline First: A Flexible and Accurate Mechanism for Pro-
portional Share Resource Allocation” by Ion Stoica and Hussein Abde l-Wahab. Technical Re-
port TR-95-22, Old Dominion University , 1996. A tech report on this cool scheduling idea, from
Ion Stoica, now a professor at U.C. Berkeley and world expert in networking, di stributed systems, and
many other things.
[TTG95] “Evaluating the Performance of Cache-Afﬁnity Scheduling in Shared-Memo ry Mul-
tiprocessors” by Josep Torrellas, Andrew Tucker, Anoop Gupta. Jou rnal of Parallel and Dis-
tributed Computing, V olume 24:2, February 1995. This is not the ﬁrst paper on the topic, but it has
citations to earlier work, and is a more readable and practical paper than some of the ear lier queuing-
based analysis papers.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

12 M ULTIPROCESSOR SCHEDULING (A DVANCED )
Homework (Simulation)
In this homework, we’ll use multi.py to simulate a multi-processor
CPU scheduler, and learn about some of its details. Read the rela ted
README for more information about the simulator and its options.
Questions
1. To start things off, let’s learn how to use the simulator to stud y how
to build an effective multi-processor scheduler. The ﬁrst sim ulation
will run just one job, which has a run-time of 30, and a working-set
size of 200. Run this job (called job ’a’ here) on one simulated CPU
as follows: ./multi.py -n 1 -L a:30:200 . How long will it
take to complete? Turn on the -c ﬂag to see a ﬁnal answer, and the
-t ﬂag to see a tick-by-tick trace of the job and how it is scheduled.
2. Now increase the cache size so as to make the job’s working set
(size=200) ﬁt into the cache (which, by default, is size=100 ); for
example, run ./multi.py -n 1 -L a:30:200 -M 300 . Can
you predict how fast the job will run once it ﬁts in cache? (hint:
remember the key parameter of the warm
rate, which is set by the
-r ﬂag) Check your answer by running with the solve ﬂag ( -c) en-
abled.
3. One cool thing about multi.py is that you can see more detail
about what is going on with different tracing ﬂags. Run the same
simulation as above, but this time with time
left tracing enabled
(-T). This ﬂag shows both the job that was scheduled on a CPU
at each time step, as well as how much run-time that job has left
after each tick has run. What do you notice about how that second
column decreases?
4. Now add one more bit of tracing, to show the status of each CPU
cache for each job, with the -C ﬂag. For each job, each cache will
either show a blank space (if the cache is cold for that job) or a ’w’
(if the cache is warm for that job). At what point does the cache
become warm for job ’a’ in this simple example? What happens
as you change the warmup
time parameter ( -w) to lower or higher
values than the default?
5. At this point, you should have a good idea of how the simula-
tor works for a single job running on a single CPU. But hey , isn’t
this a multi-processor CPU scheduling chapter? Oh yeah! So let’s
start working with multiple jobs. Speciﬁcally , let’s run the foll ow-
ing three jobs on a two-CPU system (i.e., type ./multi.py -n
2 -L a:100:100,b:100:50,c:100:50 ) Can you predict how
long this will take, given a round-robin centralized scheduler ? Use
-c to see if you were right, and then dive down into details with -t
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

MULTIPROCESSOR SCHEDULING (A DVANCED ) 13
to see a step-by-step and then -C to see whether caches got warmed
effectively for these jobs. What do you notice?
6. Now we’ll apply some explicit controls to study cache afﬁnity , as
described in the chapter. To do this, you’ll need the -A ﬂag. This
ﬂag can be used to limit which CPUs the scheduler can place a pa r-
ticular job upon. In this case, let’s use it to place jobs ’b’ and ’c’ on
CPU 1, while restricting ’a’ to CPU 0. This magic is accomplishe d
by typing this ./multi.py -n 2 -L a:100:100,b:100:50,
c:100:50 -A a:0,b:1,c:1 ; don’t forget to turn on various trac-
ing options to see what is really happening! Can you predict how
fast this version will run? Why does it do better? Will other com-
binations of ’a’, ’b’, and ’c’ onto the two processors run faster or
slower?
7. One interesting aspect of caching multiprocessors is the oppor tu-
nity for better-than-expected speed up of jobs when using multi -
ple CPUs (and their caches) as compared to running jobs on a sin-
gle processor. Speciﬁcally , when you run on N CPUs, sometimes
you can speed up by more than a factor of N , a situation entitled
super-linear speedup. To experiment with this, use the job descrip-
tion here (-L a:100:100,b:100:100,c:100:100 ) with a small
cache ( -M 50 ) to create three jobs. Run this on systems with 1, 2,
and 3 CPUs ( -n 1 , -n 2 , -n 3 ). Now, do the same, but with a
larger per-CPU cache of size 100. What do you notice about per-
formance as the number of CPUs scales? Use -c to conﬁrm your
guesses, and other tracing ﬂags to dive even deeper.
8. One other aspect of the simulator worth studying is the per-CPU
scheduling option, the -p ﬂag. Run with two CPUs again, and this
three job conﬁguration ( -L a:100:100,b:100:50,c:100:50 ).
How does this option do, as opposed to the hand-controlled afﬁnity
limits you put in place above? How does performance change as
you alter the ’peek interval’ ( -P) to lower or higher values? How
does this per-CPU approach work as the number of CPUs scales?
9. Finally , feel free to just generate random workloads and see i f you
can predict their performance on different numbers of processors ,
cache sizes, and scheduling options. If you do this, you’ll soon be
a multi-processor scheduling master , which is a pretty awesome
thing to be. Good luck!
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES
