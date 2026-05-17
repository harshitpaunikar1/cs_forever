Title: intro.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/intro.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:43+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

2
Introduction to Operating Systems
If you are taking an undergraduate operating systems course, you
should already have some idea of what a computer program does when
it runs. If not, this book (and the corresponding course) is going to b e
difﬁcult — so you should probably stop reading this book, or run to the
nearest bookstore and quickly consume the necessary background m ate-
rial before continuing (both Patt & Patel [PP03] and Bryant & O’Ha llaron
[BOH10] are pretty great books).
So what happens when a program runs?
Well, a running program does one very simple thing: it executes i n-
structions. Many millions (and these days, even billions) of tim es ev-
ery second, the processor fetches an instruction from memory , decodes
it (i.e., ﬁgures out which instruction this is), and executes it (i.e., it does
the thing that it is supposed to do, like add two numbers together , access
memory , check a condition, jump to a function, and so forth). After it is
done with this instruction, the processor moves on to the next instruction,
and so on, and so on, until the program ﬁnally completes 1.
Thus, we have just described the basics of the V on Neumannmodel of
computing2. Sounds simple, right? But in this class, we will be learning
that while a program runs, a lot of other wild things are going on with
the primary goal of making the system easy to use.
There is a body of software, in fact, that is responsible for making it
easy to run programs (even allowing you to seemingly run many at t he
same time), allowing programs to share memory , enabling program s to
interact with devices, and other fun stuff like that. That body of software
1Of course, modern processors do many bizarre and frightening things under neath the
hood to make programs run faster, e.g., executing multiple instru ctions at once, and even issu-
ing and completing them out of order! But that is not our concern here; we ar e just concerned
with the simple model most programs assume: that instructions see mingly execute one at a
time, in an orderly and sequential fashion.
2V on Neumann was one of the early pioneers of computing systems. He al so did pioneer-
ing work on game theory and atomic bombs, and played in the NBA for six years. OK, one of
those things isn’t true.
1

2 I NTRODUCTION TO OPERATING SYSTEMS
THE CRUX OF THE PROBLEM :
HOW TO VIRTUALIZE RESOURCES
One central question we will answer in this book is quite simple: how
does the operating system virtualize resources? This is the cru x of our
problem. Why the OS does this is not the main question, as the answer
should be obvious: it makes the system easier to use. Thus, we focu s on
the how: what mechanisms and policies are implemented by the OS to
attain virtualization? How does the OS do so efﬁciently? What ha rdware
support is needed?
We will use the “crux of the problem”, in shaded boxes such as this one,
as a way to call out speciﬁc problems we are trying to solve in buil ding
an operating system. Thus, within a note on a particular topic, you may
ﬁnd one or more cruces (yes, this is the proper plural) which highlight the
problem. The details within the chapter, of course, present the solution,
or at least the basic parameters of a solution.
is called the operating system (OS)3, as it is in charge of making sure the
system operates correctly and efﬁciently in an easy-to-use man ner.
The primary way the OS does this is through a general technique t hat
we call virtualization. That is, the OS takes a physical resource (such as
the processor, or memory , or a disk) and transforms it into a more gen-
eral, powerful, and easy-to-use virtual form of itself. Thus, we sometimes
refer to the operating system as a virtual machine.
Of course, in order to allow users to tell the OS what to do and thus
make use of the features of the virtual machine (such as running a pro-
gram, or allocating memory , or accessing a ﬁle), the OS also provid es
some interfaces (APIs) that you can call. A typical OS, in fact, e xports
a few hundred system calls that are available to applications. Because
the OS provides these calls to run programs, access memory and de vices,
and other related actions, we also sometimes say that the OS provi des a
standard library to applications.
Finally , because virtualization allows many programs to run (thus shar-
ing the CPU), and many programs to concurrently access their own in-
structions and data (thus sharing memory), and many programs to access
devices (thus sharing disks and so forth), the OS is sometimes k nown as
a resource manager . Each of the CPU, memory , and disk is a resource
of the system; it is thus the operating system’s role to manage those re-
sources, doing so efﬁciently or fairly or indeed with many other pos sible
goals in mind. To understand the role of the OS a little bit better , let’s take
a look at some examples.
3Another early name for the OS was the supervisor or even the master control program .
Apparently , the latter sounded a little overzealous (see the movi e Tron for details) and thus,
thankfully , “operating system” caught on instead.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

INTRODUCTION TO OPERATING SYSTEMS 3
1 #include <stdio.h>
2 #include <stdlib.h>
3 #include <sys/time.h>
4 #include <assert.h>
5 #include "common.h"
6
7 int
8 main(int argc, char *argv[])
9 {
10 if (argc != 2) {
11 fprintf(stderr, "usage: cpu <string>\n");
12 exit(1);
13 }
14 char *str = argv[1];
15 while (1) {
16 Spin(1);
17 printf("%s\n", str);
18 }
19 return 0;
20 }
Figure 2.1: Simple Example: Code That Loops And Prints ( cpu.c)
2.1 Virtualizing The CPU
Figure 2.1 depicts our ﬁrst program. It doesn’t do much. In fact, a ll
it does is call Spin(), a function that repeatedly checks the time and
returns once it has run for a second. Then, it prints out the string that the
user passed in on the command line, and repeats, forever.
Let’s say we save this ﬁle as cpu.c and decide to compile and run it
on a system with a single processor (or CPU as we will sometimes call it).
Here is what we will see:
prompt> gcc -o cpu cpu.c -Wall
prompt> ./cpu "A"
A
A
A
A
ˆC
prompt>
Not too interesting of a run — the system begins running the progra m,
which repeatedly checks the time until a second has elapsed. O nce a sec-
ond has passed, the code prints the input string passed in by the user (in
this example, the letter “A”), and continues. Note the program w ill run
forever; by pressing “Control-c” (which on U NIX -based systems will ter-
minate the program running in the foreground) we can halt the prog ram.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

4 I NTRODUCTION TO OPERATING SYSTEMS
prompt> ./cpu A & ./cpu B & ./cpu C & ./cpu D &
[1] 7353
[2] 7354
[3] 7355
[4] 7356
A
B
D
C
A
B
D
C
A
...
Figure 2.2: Running Many Programs At Once
Now, let’s do the same thing, but this time, let’s run many differ ent in-
stances of this same program. Figure 2.2 shows the results of this slightly
more complicated example.
Well, now things are getting a little more interesting. Even th ough we
have only one processor, somehow all four of these programs seem to be
running at the same time! How does this magic happen? 4
It turns out that the operating system, with some help from the har d-
ware, is in charge of this illusion, i.e., the illusion that the system has
a very large number of virtual CPUs. Turning a single CPU (or a sm all
set of them) into a seemingly inﬁnite number of CPUs and thus all owing
many programs to seemingly run at once is what we call virtualizing the
CPU, the focus of the ﬁrst major part of this book.
Of course, to run programs, and stop them, and otherwise tell the O S
which programs to run, there need to be some interfaces (APIs) t hat you
can use to communicate your desires to the OS. We’ll talk about thes e
APIs throughout this book; indeed, they are the major way in which m ost
users interact with operating systems.
You might also notice that the ability to run multiple programs a t once
raises all sorts of new questions. For example, if two programs wan t to
run at a particular time, which should run? This question is answered by
a policy of the OS; policies are used in many different places within an
OS to answer these types of questions, and thus we will study the m as
we learn about the basic mechanisms that operating systems implement
(such as the ability to run multiple programs at once). Hence th e role of
the OS as a resource manager.
4Note how we ran four processes at the same time, by using the & symbol. Doing so runs a
job in the background in the zsh shell, which means that the user is able to immediately issue
their next command, which in this case is another program to run. If you’re using a different
shell (e.g., tcsh), it works slightly differently; read documentation online for detai ls.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

INTRODUCTION TO OPERATING SYSTEMS 5
1 #include <unistd.h>
2 #include <stdio.h>
3 #include <stdlib.h>
4 #include "common.h"
5
6 int
7 main(int argc, char *argv[])
8 {
9 int *p = malloc(sizeof(int)); // a1
10 assert(p != NULL);
11 printf("(%d) address pointed to by p: %p\n",
12 getpid(), p); // a2
13 *p = 0; // a3
14 while (1) {
15 Spin(1);
16 *p = *p + 1;
17 printf("(%d) p: %d\n", getpid(), *p); // a4
18 }
19 return 0;
20 }
Figure 2.3: A Program That Accesses Memory ( mem.c)
2.2 Virtualizing Memory
Now let’s consider memory . The model of physical memory pre-
sented by modern machines is very simple. Memory is just an arra y of
bytes; to read memory , one must specify an address to be able to access
the data stored there; to write (or update) memory , one must also specify
the data to be written to the given address.
Memory is accessed all the time when a program is running. A pro-
gram keeps all of its data structures in memory , and accesses them through
various instructions, like loads and stores or other explicit inst ructions
that access memory in doing their work. Don’t forget that each instr uc-
tion of the program is in memory too; thus memory is accessed on each
instruction fetch.
Let’s take a look at a program (in Figure 2.3) that allocates some mem -
ory by calling malloc(). The output of this program can be found here:
prompt> ./mem
(2134) address pointed to by p: 0x200000
(2134) p: 1
(2134) p: 2
(2134) p: 3
(2134) p: 4
(2134) p: 5
ˆC
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

6 I NTRODUCTION TO OPERATING SYSTEMS
prompt> ./mem & ./mem &
[1] 24113
[2] 24114
(24113) address pointed to by p: 0x200000
(24114) address pointed to by p: 0x200000
(24113) p: 1
(24114) p: 1
(24114) p: 2
(24113) p: 2
(24113) p: 3
(24114) p: 3
(24113) p: 4
(24114) p: 4
...
Figure 2.4: Running The Memory Program Multiple Times
The program does a couple of things. First, it allocates some memory
(line a1). Then, it prints out the address of the memory (a2), and then
puts the number zero into the ﬁrst slot of the newly allocated mem ory
(a3). Finally , it loops, delaying for a second and incrementing t he value
stored at the address held in p. With every print statement, it also prints
out what is called the process identiﬁer (the PID) of the running program.
This PID is unique per running process.
Again, this ﬁrst result is not too interesting. The newly alloca ted mem-
ory is at address 0x200000. As the program runs, it slowly updates the
value and prints out the result.
Now, we again run multiple instances of this same program to see
what happens (Figure 2.4). We see from the example that each ru nning
program has allocated memory at the same address ( 0x200000), and yet
each seems to be updating the value at 0x200000 independently! It is as
if each running program has its own private memory , instead of sha ring
the same physical memory with other running programs 5.
Indeed, that is exactly what is happening here as the OS is virtualiz-
ing memory. Each process accesses its own private virtual address space
(sometimes just called its address space ), which the OS somehow maps
onto the physical memory of the machine. A memory reference withi n
one running program does not affect the address space of other proces ses
(or the OS itself); as far as the running program is concerned, it has phys-
ical memory all to itself. The reality , however, is that physic al memory is
a shared resource, managed by the operating system. Exactly how all of
this is accomplished is also the subject of the ﬁrst part of this b ook, on the
topic of virtualization.
5For this example to work, you need to make sure address-space rando mization is dis-
abled; randomization, as it turns out, can be a good defense against ce rtain kinds of security
ﬂaws. Read more about it on your own, especially if you want to lea rn how to break into
computer systems via stack-smashing attacks. Not that we would recom mend such a thing...
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

INTRODUCTION TO OPERATING SYSTEMS 7
2.3 Concurrency
1 #include <stdio.h>
2 #include <stdlib.h>
3 #include "common.h"
4 #include "common_threads.h"
5
6 volatile int counter = 0;
7 int loops;
8
9 void *worker(void *arg) {
10 int i;
11 for (i = 0; i < loops; i++) {
12 counter++;
13 }
14 return NULL;
15 }
16
17 int main(int argc, char *argv[]) {
18 if (argc != 2) {
19 fprintf(stderr, "usage: threads <value>\n");
20 exit(1);
21 }
22 loops = atoi(argv[1]);
23 pthread_t p1, p2;
24 printf("Initial value : %d\n", counter);
25
26 Pthread_create(&p1, NULL, worker, NULL);
27 Pthread_create(&p2, NULL, worker, NULL);
28 Pthread_join(p1, NULL);
29 Pthread_join(p2, NULL);
30 printf("Final value : %d\n", counter);
31 return 0;
32 }
Figure 2.5: A Multi-threaded Program ( threads.c)
Another main theme of this book is concurrency. We use this concep-
tual term to refer to a host of problems that arise, and must be add ressed,
when working on many things at once (i.e., concurrently) in the sa me
program. The problems of concurrency arose ﬁrst within the operati ng
system itself; as you can see in the examples above on virtualiza tion, the
OS is juggling many things at once, ﬁrst running one process, the n an-
other, and so forth. As it turns out, doing so leads to some deep and
interesting problems.
Unfortunately , the problems of concurrency are no longer limited just
to the OS itself. Indeed, modern multi-threaded programs exhibit the
same problems. Let us demonstrate with an example of a multi-threaded
program (Figure 2.5).
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

8 I NTRODUCTION TO OPERATING SYSTEMS
Although you might not understand this example fully at the momen t
(and we’ll learn a lot more about it in later chapters, in the secti on of the
book on concurrency), the basic idea is simple. The main program cr eates
two threads using Pthread_create()6. You can think of a thread as a
function running within the same memory space as other functions , with
more than one of them active at a time. In this example, each threa d starts
running in a routine called worker(), in which it simply increments a
counter in a loop for loops number of times.
Below is a transcript of what happens when we run this program wit h
the input value for the variable loops set to 1000. The value of loops
determines how many times each of the two workers will increment the
shared counter in a loop. When the program is run with the value of
loops set to 1000, what do you expect the ﬁnal value of counter to be?
prompt> gcc -o threads threads.c -Wall -pthread
prompt> ./threads 1000
Initial value : 0
Final value : 2000
As you probably guessed, when the two threads are ﬁnished, the ﬁ nal
value of the counter is 2000, as each thread incremented the coun ter 1000
times. Indeed, when the input value of loops is set to N , we would
expect the ﬁnal output of the program to be 2N . But life is not so simple,
as it turns out. Let’s run the same program, but with higher value s for
loops, and see what happens:
prompt> ./threads 100000
Initial value : 0
Final value : 143012 // huh??
prompt> ./threads 100000
Initial value : 0
Final value : 137298 // what the??
In this run, when we gave an input value of 100,000, instead of ge tting
a ﬁnal value of 200,000, we instead ﬁrst get 143,012. Then, whe n we run
the program a second time, we not only again get the wrong value, but
also a different value than the last time. In fact, if you run the program
over and over with high values of loops, you may ﬁnd that sometimes
you even get the right answer! So why is this happening?
As it turns out, the reason for these odd and unusual outcomes relate
to how instructions are executed, which is one at a time. Unfortun ately , a
key part of the program above, where the shared counter is increme nted,
6The actual call should be to lower-case pthread_create(); the upper-case version is
our own wrapper that calls pthread_create() and makes sure that the return code indi-
cates that the call succeeded. See the code for details.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

INTRODUCTION TO OPERATING SYSTEMS 9
THE CRUX OF THE PROBLEM :
HOW TO BUILD CORRECT CONCURRENT PROGRAMS
When there are many concurrently executing threads within th e same
memory space, how can we build a correctly working program? What
primitives are needed from the OS? What mechanisms should be pro-
vided by the hardware? How can we use them to solve the problems of
concurrency?
takes three instructions: one to load the value of the counter from m em-
ory into a register, one to increment it, and one to store it back in to mem-
ory . Because these three instructions do not execute atomically (all at
once), strange things can happen. It is this problem of concurrency that
we will address in great detail in the second part of this book.
2.4 Persistence
The third major theme of the course is persistence. In system memory ,
data can be easily lost, as devices such as DRAM store values in a volatile
manner; when power goes away or the system crashes, any data in me m-
ory is lost. Thus, we need hardware and software to be able to store data
persistently; such storage is thus critical to any system as users care a
great deal about their data.
The hardware comes in the form of some kind of input/output or I/O
device; in modern systems, a hard drive is a common repository for long-
lived information, although solid-state drives (SSDs) are making head-
way in this arena as well.
The software in the operating system that usually manages the d isk is
called the ﬁle system ; it is thus responsible for storing any ﬁles the user
creates in a reliable and efﬁcient manner on the disks of the sys tem.
Unlike the abstractions provided by the OS for the CPU and memory ,
the OS does not create a private, virtualized disk for each appli cation.
Rather, it is assumed that often times, users will want to share informa-
tion that is in ﬁles. For example, when writing a C program, you mig ht
ﬁrst use an editor (e.g., Emacs 7) to create and edit the C ﬁle ( emacs -nw
main.c). Once done, you might use the compiler to turn the source code
into an executable (e.g., gcc -o main main.c ). When you’re ﬁnished,
you might run the new executable (e.g., ./main). Thus, you can see how
ﬁles are shared across different processes. First, Emacs crea tes a ﬁle that
serves as input to the compiler; the compiler uses that input ﬁl e to create
a new executable ﬁle (in many steps — take a compiler course for de tails);
ﬁnally , the new executable is then run. And thus a new program i s born!
7You should be using Emacs. If you are using vi, there is probably som ething wrong with
you. If you are using something that is not a real code editor, that is e ven worse.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

10 I NTRODUCTION TO OPERATING SYSTEMS
1 #include <stdio.h>
2 #include <unistd.h>
3 #include <assert.h>
4 #include <fcntl.h>
5 #include <sys/types.h>
6
7 int main(int argc, char *argv[]) {
8 int fd = open("/tmp/file",
9 O_WRONLY|O_CREAT|O_TRUNC,
10 S_IRWXU);
11 assert(fd > -1);
12 int rc = write(fd, "hello world\n", 12);
13 assert(rc == 12);
14 close(fd);
15 return 0;
16 }
Figure 2.6: A Program That Does I/O ( io.c)
To understand this better, let’s look at some code. Figure 2.6 pres ents
code to create a ﬁle ( /tmp/file) that contains the string “hello world”.
To accomplish this task, the program makes three calls into the oper-
ating system. The ﬁrst, a call to open(), opens the ﬁle and creates it; the
second, write(), writes some data to the ﬁle; the third, close(), sim-
ply closes the ﬁle thus indicating the program won’t be writing an y more
data to it. These system calls are routed to the part of the operating sys-
tem called the ﬁle system , which then handles the requests and returns
some kind of error code to the user.
You might be wondering what the OS does in order to actually write
to disk. We would show you but you’d have to promise to close your
eyes ﬁrst; it is that unpleasant. The ﬁle system has to do a fai r bit of work:
ﬁrst ﬁguring out where on disk this new data will reside, and the n keep-
ing track of it in various structures the ﬁle system maintains. Doing so
requires issuing I/O requests to the underlying storage devi ce, to either
read existing structures or update (write) them. As anyone who has writ-
ten a device driver 8 knows, getting a device to do something on your
behalf is an intricate and detailed process. It requires a dee p knowledge
of the low-level device interface and its exact semantics. Fort unately , the
OS provides a standard and simple way to access devices through its sys-
tem calls. Thus, the OS is sometimes seen as a standard library.
Of course, there are many more details in how devices are accesse d,
and how ﬁle systems manage data persistently atop said devices . For
performance reasons, most ﬁle systems ﬁrst delay such writes for a while,
hoping to batch them into larger groups. To handle the problems of sys-
tem crashes during writes, most ﬁle systems incorporate some kin d of
8A device driver is some code in the operating system that knows how to d eal with a
speciﬁc device. We will talk more about devices and device drivers later.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

INTRODUCTION TO OPERATING SYSTEMS 11
THE CRUX OF THE PROBLEM :
HOW TO STORE DATA PERSISTENTLY
The ﬁle system is the part of the OS in charge of managing persist ent data.
What techniques are needed to do so correctly? What mechanism s and
policies are required to do so with high performance? How is reli ability
achieved, in the face of failures in hardware and software?
intricate write protocol, such as journaling or copy-on-write, carefully
ordering writes to disk to ensure that if a failure occurs durin g the write
sequence, the system can recover to reasonable state afterwar ds. To make
different common operations efﬁcient, ﬁle systems employ many di ffer-
ent data structures and access methods, from simple lists to com plex b-
trees. If all of this doesn’t make sense yet, good! We’ll be talking a bout
all of this quite a bit more in the third part of this book on persistence,
where we’ll discuss devices and I/O in general, and then disks , RAIDs,
and ﬁle systems in great detail.
2.5 Design Goals
So now you have some idea of what an OS actually does: it takes phys-
ical resources, such as a CPU, memory , or disk, and virtualizes them. It
handles tough and tricky issues related to concurrency. And it stores ﬁles
persistently, thus making them safe over the long-term. Given that we
want to build such a system, we want to have some goals in mind to h elp
focus our design and implementation and make trade-offs as neces sary;
ﬁnding the right set of trade-offs is a key to building systems.
One of the most basic goals is to build up some abstractions in order
to make the system convenient and easy to use. Abstractions are fun-
damental to everything we do in computer science. Abstraction makes
it possible to write a large program by dividing it into small an d under-
standable pieces, to write such a program in a high-level lang uage like
C9 without thinking about assembly , to write code in assembly with out
thinking about logic gates, and to build a processor out of gates wit hout
thinking too much about transistors. Abstraction is so fundamen tal that
sometimes we forget its importance, but we won’t here; thus, in eac h sec-
tion, we’ll discuss some of the major abstractions that have develop ed
over time, giving you a way to think about pieces of the OS.
One goal in designing and implementing an operating system is t o
provide high performance; another way to say this is our goal is to mini-
mize the overheads of the OS. Virtualization and making the system easy
to use are well worth it, but not at any cost; thus, we must strive t o pro-
9Some of you might object to calling C a high-level language. Remember t his is an OS
course, though, where we’re simply happy not to have to code in assembl y all the time!
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

12 I NTRODUCTION TO OPERATING SYSTEMS
vide virtualization and other OS features without excessive ove rheads.
These overheads arise in a number of forms: extra time (more instr uc-
tions) and extra space (in memory or on disk). We’ll seek solutions th at
minimize one or the other or both, if possible. Perfection, however, i s not
always attainable, something we will learn to notice and (wher e appro-
priate) tolerate.
Another goal will be to provide protection between applications, as
well as between the OS and applications. Because we wish to all ow
many programs to run at the same time, we want to make sure that t he
malicious or accidental bad behavior of one does not harm others; we
certainly don’t want an application to be able to harm the OS itse lf (as
that would affect all programs running on the system). Protection is at
the heart of one of the main principles underlying an operating sy stem,
which is that of isolation; isolating processes from one another is the key
to protection and thus underlies much of what an OS must do.
The operating system must also run non-stop; when it fails, all appli-
cations running on the system fail as well. Because of this depen dence,
operating systems often strive to provide a high degree of reliability. As
operating systems grow evermore complex (sometimes containing mi l-
lions of lines of code), building a reliable operating system is qu ite a chal-
lenge — and indeed, much of the on-going research in the ﬁeld (inc luding
some of our own work [BS+09, SS+10]) focuses on this exact problem.
Other goals make sense: energy-efﬁciency is important in our increas-
ingly green world; security (an extension of protection, really) against
malicious applications is critical, especially in these high ly-networked
times; mobility is increasingly important as OSes are run on smaller and
smaller devices. Depending on how the system is used, the OS wil l have
different goals and thus likely be implemented in at least sli ghtly differ-
ent ways. However, as we will see, many of the principles we will present
on how to build an OS are useful on a range of different devices.
2.6 Some History
Before closing this introduction, let us present a brief history of how
operating systems developed. Like any system built by humans, good
ideas accumulated in operating systems over time, as engineer s learned
what was important in their design. Here, we discuss a few major devel-
opments. For a richer treatment, see Brinch Hansen’s excellent history of
operating systems [BH00].
Early Operating Systems: Just Libraries
In the beginning, the operating system didn’t do too much. Basic ally ,
it was just a set of libraries of commonly-used functions; for examp le,
instead of having each programmer of the system write low-level I /O
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

INTRODUCTION TO OPERATING SYSTEMS 13
handling code, the “OS” would provide such APIs, and thus make lif e
easier for the developer.
Usually , on these old mainframe systems, one program ran at a time ,
as controlled by a human operator. Much of what you think a modern
OS would do (e.g., deciding what order to run jobs in) was performe d by
this operator. If you were a smart developer, you would be nice to thi s
operator, so that they might move your job to the front of the queue.
This mode of computing was known as batch processing, as a number
of jobs were set up and then run in a “batch” by the operator. Compute rs,
as of that point, were not used in an interactive manner, because of cost:
it was simply too expensive to let a user sit in front of the compute r and
use it, as most of the time it would just sit idle then, costing the f acility
hundreds of thousands of dollars per hour [BH00].
Beyond Libraries: Protection
In moving beyond being a simple library of commonly-used services , op-
erating systems took on a more central role in managing machines. O ne
important aspect of this was the realization that code run on behal f of the
OS was special; it had control of devices and thus should be treate d dif-
ferently than normal application code. Why is this? Well, imagi ne if you
allowed any application to read from anywhere on the disk; the noti on of
privacy goes out the window, as any program could read any ﬁle. Thus ,
implementing a ﬁle system (to manage your ﬁles) as a library makes little
sense. Instead, something else was needed.
Thus, the idea of a system call was invented, pioneered by the Atlas
computing system [K+61,L78]. Instead of providing OS routines a s a li-
brary (where you just make a procedure call to access them), the idea here
was to add a special pair of hardware instructions and hardware state to
make the transition into the OS a more formal, controlled process.
The key difference between a system call and a procedure call i s that
a system call transfers control (i.e., jumps) into the OS while simultane-
ously raising the hardware privilege level. User applications run in what
is referred to as user mode which means the hardware restricts what ap-
plications can do; for example, an application running in user mod e can’t
typically initiate an I/O request to the disk, access any phy sical memory
page, or send a packet on the network. When a system call is initia ted
(usually through a special hardware instruction called a trap), the hard-
ware transfers control to a pre-speciﬁed trap handler (that the OS set up
previously) and simultaneously raises the privilege level to kernel mode.
In kernel mode, the OS has full access to the hardware of the syst em and
thus can do things like initiate an I/O request or make more memor y
available to a program. When the OS is done servicing the reques t, it
passes control back to the user via a special return-from-trap instruction,
which reverts to user mode while simultaneously passing control back to
where the application left off.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

14 I NTRODUCTION TO OPERATING SYSTEMS
The Era of Multiprogramming
Where operating systems really took off was in the era of computing b e-
yond the mainframe, that of the minicomputer. Classic machines like
the PDP family from Digital Equipment made computers hugely mor e
affordable; thus, instead of having one mainframe per large orga nization,
now a smaller collection of people within an organization could likel y
have their own computer. Not surprisingly , one of the major impacts of
this drop in cost was an increase in developer activity; more smar t people
got their hands on computers and thus made computer systems do more
interesting and beautiful things.
In particular, multiprogramming became commonplace due to the de-
sire to make better use of machine resources. Instead of just run ning one
job at a time, the OS would load a number of jobs into memory and switch
rapidly between them, thus improving CPU utilization. This sw itching
was particularly important because I/O devices were slow; hav ing a pro-
gram wait on the CPU while its I/O was being serviced was a waste of
CPU time. Instead, why not switch to another job and run it for a whi le?
The desire to support multiprogramming and overlap in the prese nce
of I/O and interrupts forced innovation in the conceptual development of
operating systems along a number of directions. Issues such as memory
protection became important; we wouldn’t want one program to be able
to access the memory of another program. Understanding how to deal
with the concurrency issues introduced by multiprogramming was also
critical; making sure the OS was behaving correctly despite t he presence
of interrupts is a great challenge. We will study these issues and related
topics later in the book.
One of the major practical advances of the time was the introducti on
of the U NIX operating system, primarily thanks to Ken Thompson (and
Dennis Ritchie) at Bell Labs (yes, the phone company). U NIX took many
good ideas from different operating systems (particularly from M ultics
[O72], and some from systems like TENEX [B+72] and the Berkeley Time-
Sharing System [S68]), but made them simpler and easier to use. Soon this
team was shipping tapes containing U NIX source code to people around
the world, many of whom then got involved and added to the system
themselves; see the Aside (next page) for more detail 10.
The Modern Era
Beyond the minicomputer came a new type of machine, cheaper, fas ter,
and for the masses: the personal computer, or PC as we call it today . Led
by Apple’s early machines (e.g., the Apple II) and the IBM PC, t his new
breed of machine would soon become the dominant force in computing,
10We’ll use asides and other related text boxes to call attention to various items that don’t
quite ﬁt the main ﬂow of the text. Sometimes, we’ll even use them j ust to make a joke, because
why not have a little fun along the way? Yes, many of the jokes are bad.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

INTRODUCTION TO OPERATING SYSTEMS 15
ASIDE : T HE IMPORTANCE OF UNIX
It is difﬁcult to overstate the importance of U NIX in the history of oper-
ating systems. Inﬂuenced by earlier systems (in particular , the famous
Multics system from MIT), U NIX brought together many great ideas and
made a system that was both simple and powerful.
Underlying the original “Bell Labs” U NIX was the unifying principle of
building small powerful programs that could be connected togethe r to
form larger workﬂows. The shell, where you type commands, provided
primitives such as pipes to enable such meta-level programming, and
thus it became easy to string together programs to accomplish a b ig-
ger task. For example, to ﬁnd lines of a text ﬁle that have the word
“foo” in them, and then to count how many such lines exist, you would
type: grep foo file.txt|wc -l , thus using the grep and wc (word
count) programs to achieve your task.
The U NIX environment was friendly for programmers and developers
alike, also providing a compiler for the new C programming language .
Making it easy for programmers to write their own programs, as wel l as
share them, made U NIX enormously popular. And it probably helped a
lot that the authors gave out copies for free to anyone who asked, an e arly
form of open-source software.
Also of critical importance was the accessibility and readabi lity of the
code. Having a beautiful, small kernel written in C invited oth ers to play
with the kernel, adding new and cool features. For example, an en ter-
prising group at Berkeley , led by Bill Joy, made a wonderful distribution
(the Berkeley Systems Distribution, or BSD) which had some advanced
virtual memory , ﬁle system, and networking subsystems. Joy lat er co-
founded Sun Microsystems.
Unfortunately , the spread of UNIX was slowed a bit as companies tried to
assert ownership and proﬁt from it, an unfortunate (but common) res ult
of lawyers getting involved. Many companies had their own varian ts:
SunOS from Sun Microsystems, AIX from IBM, HPUX (a.k.a. “H-Pucks”)
from HP , and IRIX from SGI. The legal wrangling among AT&T/Bell
Labs and these other players cast a dark cloud over U NIX , and many
wondered if it would survive, especially as Windows was introduced and
took over much of the PC market...
as their low-cost enabled one machine per desktop instead of a shar ed
minicomputer per workgroup.
Unfortunately , for operating systems, the PC at ﬁrst represent ed a
great leap backwards, as early systems forgot (or never knew of) t he
lessons learned in the era of minicomputers. For example, early op erat-
ing systems such as DOS (the Disk Operating System , from Microsoft)
didn’t think memory protection was important; thus, a malicious (or per-
haps just a poorly-programmed) application could scribble all ove r mem-
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

16 I NTRODUCTION TO OPERATING SYSTEMS
ASIDE : A ND THEN CAME LINUX
Fortunately for U NIX , a young Finnish hacker named Linus T orvaldsde-
cided to write his own version of U NIX which borrowed heavily on the
principles and ideas behind the original system, but not from th e code
base, thus avoiding issues of legality . He enlisted help from ma ny others
around the world, took advantage of the sophisticated GNU tools that
already existed [G85], and soon Linux was born (as well as the modern
open-source software movement).
As the internet era came into place, most companies (such as Googl e,
Amazon, Facebook, and others) chose to run Linux, as it was free and
could be readily modiﬁed to suit their needs; indeed, it is hard to imag-
ine the success of these new companies had such a system not exist ed.
As smart phones became a dominant user-facing platform, Linux f ound
a stronghold there too (via Android), for many of the same reasons. An d
Steve Jobs took his U NIX -based NeXTStep operating environment with
him to Apple, thus making U NIX popular on desktops (though many
users of Apple technology are probably not even aware of this fact). Thus
UNIX lives on, more important today than ever before. The computing
gods, if you believe in them, should be thanked for this wonderful ou t-
come.
ory . The ﬁrst generations of the Mac OS (v9 and earlier) took a coopera-
tive approach to job scheduling; thus, a thread that accidenta lly got stuck
in an inﬁnite loop could take over the entire system, forcing a reboot . The
painful list of OS features missing in this generation of system s is long,
too long for a full discussion here.
Fortunately , after some years of suffering, the old features of mi ni-
computer operating systems started to ﬁnd their way onto the des ktop.
For example, Mac OS X/macOS has U NIX at its core, including all of the
features one would expect from such a mature system. Windows has sim-
ilarly adopted many of the great ideas in computing history , star ting in
particular with Windows NT, a great leap forward in Microsoft OS t ech-
nology . Even today’s cell phones run operating systems (such as Lin ux)
that are much more like what a minicomputer ran in the 1970s than what
a PC ran in the 1980s (thank goodness); it is good to see that the good
ideas developed in the heyday of OS development have found their w ay
into the modern world. Even better is that these ideas continue t o de-
velop, providing more features and making modern systems even be tter
for users and applications.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

INTRODUCTION TO OPERATING SYSTEMS 17
2.7 Summary
Thus, we have an introduction to the OS. Today’s operating systems
make systems relatively easy to use, and virtually all operat ing systems
you use today have been inﬂuenced by the developments we will dis cuss
throughout the book.
Unfortunately , due to time constraints, there are a number of pa rts of
the OS we won’t cover in the book. For example, there is a lot of net-
working code in the operating system; we leave it to you to take the net-
working class to learn more about that. Similarly , graphics devices are
particularly important; take the graphics course to expand you r knowl-
edge in that direction. Finally , some operating system books talk a great
deal about security; we will do so in the sense that the OS must provide
protection between running programs and give users the ability to pro-
tect their ﬁles, but we won’t delve into deeper security issues that one
might ﬁnd in a security course.
However, there are many important topics that we will cover, incl ud-
ing the basics of virtualization of the CPU and memory , concurrency , and
persistence via devices and ﬁle systems. Don’t worry! While the re is a
lot of ground to cover, most of it is quite cool, and at the end of the road,
you’ll have a new appreciation for how computer systems really work.
Now get to work!
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

18 I NTRODUCTION TO OPERATING SYSTEMS
References
[BS+09] “Tolerating File-System Mistakes with EnvyFS” by L. Bair avasundaram, S. Sundarara-
man, A. Arpaci-Dusseau, R. Arpaci-Dusseau. USENIX ’09, San Diego , CA, June 2009. A fun
paper about using multiple ﬁle systems at once to tolerate a mistake in any one of the m.
[BH00] “The Evolution of Operating Systems” by P . Brinch Hansen. In ’Cl assic Operating
Systems: From Batch Processing to Distributed Systems.’ Springe r-V erlag, New York, 2000.
This essay provides an intro to a wonderful collection of papers about histori cally signiﬁcant systems.
[B+72] “TENEX, A Paged Time Sharing System for the PDP-10” by D. Bobrow, J. Burchﬁel, D.
Murphy , R. Tomlinson. CACM, V olume 15, Number 3, March 1972. TENEX has much of the
machinery found in modern operating systems; read more about it to see how mu ch innovation was
already in place in the early 1970’s.
[B75] “The Mythical Man-Month” by F. Brooks. Addison-Wesley , 1975. A classic text on software
engineering; well worth the read.
[BOH10] “Computer Systems: A Programmer’s Perspective” by R. Bry ant and D. O’Hallaron.
Addison-Wesley , 2010.Another great intro to how computer systems work. Has a little bit of overlap
with this book — so if you’d like, you can skip the last few chapters of that book, or sim ply read them to
get a different perspective on some of the same material. After all, one good w ay to build up your own
knowledge is to hear as many other perspectives as possible, and then develop your own opinion and
thoughts on the matter. Y ou know, by thinking!
[G85] “The GNU Manifesto” by R. Stallman. 1985. www.gnu.org/gnu/manifesto.html.
A huge part of Linux’s success was no doubt the presence of an excellen t compiler, gcc, and other
relevant pieces of open software, thanks to the GNU effort headed by Stallman. S tallman is a visionary
when it comes to open source, and this manifesto lays out his thoughts as to why.
[K+61] “One-Level Storage System” by T. Kilburn, D.B.G. Edwards, M.J. Lanigan, F.H. Sumner.
IRE Transactions on Electronic Computers, April 1962. The Atlas pioneered much of what you see
in modern systems. However, this paper is not the best read. If you were to on ly read one, you might
try the historical perspective below [L78].
[L78] “The Manchester Mark I and Atlas: A Historical Perspective” by S. H. L avington. Com-
munications of the ACM, V olume 21:1, January 1978. A nice piece of history on the early devel-
opment of computer systems and the pioneering efforts of the Atlas. Of course, one could go back and
read the Atlas papers themselves, but this paper provides a great overvie w and adds some historical
perspective.
[O72] “The Multics System: An Examination of its Structure” by Elliot t Organick. MIT Press,
1972. A great overview of Multics. So many good ideas, and yet it was an over-design ed system,
shooting for too much, and thus never really worked. A classic example of what F red Brooks would call
the “second-system effect” [B75].
[PP03] “Introduction to Computing Systems: From Bits and Gates to C a nd Beyond” by Yale
N. Patt, Sanjay J. Patel. McGraw-Hill, 2003. One of our favorite intro to computing systems books.
Starts at transistors and gets you all the way up to C; the early material is particularly great.
[RT74] “The U NIX Time-Sharing System” by Dennis M. Ritchie, Ken Thompson. CACM, V ol-
ume 17: 7, July 1974. A great summary of UNIX written as it was taking over the world of computing,
by the people who wrote it.
[S68] “SDS 940 Time-Sharing System” by Scientiﬁc Data Systems. TECH NICAL MANUAL,
SDS 90 11168, August 1968. Y es, a technical manual was the best we could ﬁnd. But it is fascinating
to read these old system documents, and see how much was already in place in the late 1960’s. One of
the minds behind the Berkeley Time-Sharing System (which eventually b ecame the SDS system) was
Butler Lampson, who later won a T uring award for his contributions in systems .
[SS+10] “Membrane: Operating System Support for Restartable File Systems” by S. Sundarara-
man, S. Subramanian, A. Rajimwale, A. Arpaci-Dusseau, R. Arpaci-Du sseau, M. Swift. FAST
’10, San Jose, CA, February 2010. The great thing about writing your own class notes: you can ad-
vertise your own research. But this paper is actually pretty neat — when a ﬁl e system hits a bug and
crashes, Membrane auto-magically restarts it, all without applications or the rest of the system being
affected.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

INTRODUCTION TO OPERATING SYSTEMS 19
Homework
Most (and eventually , all) chapters of this book have homework sec-
tions at the end. Doing these homeworks is important, as each lets y ou,
the reader, gain more experience with the concepts presented w ithin the
chapter.
There are two types of homeworks. The ﬁrst is based on simulation. A
simulation of a computer system is just a simple program that pretends to
do some of the interesting parts of what a real system does, and the n re-
port some output metrics to show how the system behaves. For example ,
a hard drive simulator might take a series of requests, simulat e how long
they would take to get serviced by a hard drive with certain per formance
characteristics, and then report the average latency of the re quests.
The cool thing about simulations is they let you easily explore how
systems behave without the difﬁculty of running a real system. Indeed,
they even let you create systems that cannot exist in the real wor ld (for
example, a hard drive with unimaginably fast performance), a nd thus see
the potential impact of future technologies.
Of course, simulations are not without their downsides. By their v ery
nature, simulations are just approximations of how a real system behaves.
If an important aspect of real-world behavior is omitted, the simu lation
will report bad results. Thus, results from a simulation should a lways be
treated with some suspicion. In the end, how a system behaves in t he real
world is what matters.
The second type of homework requires interaction with real-world
code. Some of these homeworks are measurement focused, whereas oth-
ers just require some small-scale development and experimentation. Both
are just small forays into the larger world you should be getting i nto,
which is how to write systems code in C on U NIX -based systems. Indeed,
larger-scale projects, which go beyond these homeworks, are nee ded to
push you in this direction; thus, beyond just doing homeworks, we strongly
recommend you do projects to solidify your systems skills. See this page
(https://github.com/remzi-arpacidusseau/ostep-projects)
for some projects.
To do these homeworks, you likely have to be on a U NIX -based ma-
chine, running either Linux, macOS, or some similar system. It s hould
also have a C compiler installed (e.g., gcc) as well as Python. You should
also know how to edit code in a real code editor of some kind.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES
