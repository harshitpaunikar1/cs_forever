Title: lab-tutorial.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/lab-tutorial.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:46+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

F
Laboratory: T utorial
This is a very brief document to familiarize you with the basics of the C
programming environment on U NIX systems. It is not comprehensive or
particularly detailed, but should just give you enough to get you going.
A couple of general points of advice about programming: if you want
to become an expert programmer, you need to master more than just t he
syntax of a language. Speciﬁcally , you should know your tools , know
your libraries , and know your documentation . The tools that are rel-
evant to C compilation are gcc, gdb, and maybe ld. There are tons of
library routines that are also available to you, but fortunatel y a lot of
functionality is included in libc, which is linked with all C programs by
default — all you need to do is include the right header ﬁles. Fi nally ,
knowing how to ﬁnd the library routines you need (e.g., learning t o ﬁnd
and read man pages) is a skill worth acquiring. We’ll talk about e ach of
these in more detail later on.
Like (almost) everything worth doing in life, becoming an expert in
these domains takes time. Spending the time up-front to learn more about
the tools and environment is deﬁnitely well worth the effort.
F.1 A Simple C Program
We’ll start with a simple C program, perhaps saved in the ﬁle “hw .c”.
Unlike Java, there is not necessarily a connection between the ﬁ le name
and the contents of the ﬁle; thus, use your common sense in naming ﬁl es
in a manner that is appropriate.
The ﬁrst line speciﬁes a ﬁle to include, in this case stdio.h, which
“prototypes” many of the commonly used input/output routines; the
one we are interested in is printf(). When you use the #include di-
rective, you are telling the C preprocessor ( cpp) to ﬁnd a particular ﬁle
(e.g., stdio.h) and to insert it directly into your code at the spot of the
#include. By default, cpp will look in the directory /usr/include/
to try to ﬁnd the ﬁle.
The next part speciﬁes the signature of the main() routine, namely
that it returns an integer ( int), and will be called with two arguments,
1

2 L ABORATORY : T UTORIAL
/* header files go up here */
/* note that C comments are enclosed within a slash and
a star, and may wrap over lines */
// two slashes work too (and may be preferred)
#include <stdio.h>
// main returns an integer
int main(int argc, char *argv[]) {
/* printf is our output function;
by default, writes to standard out */
/* printf returns an integer, but we ignore that */
printf("hello, world\n");
/* return 0 to indicate all went well */
return(0);
}
an integer argc, which is a count of the number of arguments on the com-
mand line, and an array of pointers to characters ( argv), each of which
contain a word from the command line, and the last of which is null.
There will be more on pointers and arrays below.
The program then simply prints the string “hello, world” and ad-
vances the output stream to the next line, courtesy of the backsl ash fol-
lowed by an “n” at the end of the call to printf(). Afterwards, the pro-
gram completes by returning a value, which is passed back to th e shell
that executed the program. A script or the user at the terminal c ould
check this value (in csh and tcsh shells, it is stored in the status vari-
able), to see whether the program exited cleanly or with an error .
F.2 Compilation and Execution
We’ll now learn how to compile the program. Note that we will use
gcc as our example, though on some platforms you may be able to use a
different (native) compiler, cc.
At the shell prompt, you just type:
prompt> gcc hw.c
gcc is not really the compiler, but rather the program called a “com-
piler driver”; thus it coordinates the many steps of the compilat ion. Usu-
ally there are four to ﬁve steps. First, gcc will execute cpp, the C pre-
processor, to process certain directives (such as#define and #include).
The program cpp is just a source-to-source translator, so its end-product
is still just source code (i.e., a C ﬁle). Then the real compilati on will begin,
usually a command called cc1. This will transform source-level C code
into low-level assembly code, speciﬁc to the host machine. The a ssem-
bler as will then be executed, generating object code (bits and things that
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LABORATORY : T UTORIAL 3
machines can really understand), and ﬁnally the link-editor (or linker) ld
will put it all together into a ﬁnal executable program. Fortuna tely(!), for
most purposes, you can blithely be unaware of how gcc works, and just
use it with the proper ﬂags.
The result of your compilation above is an executable, named (by de -
fault) a.out. To then run the program, we simply type:
prompt> ./a.out
When we run this program, the OS will set argc and argv properly
so that the program can process the command-line arguments as ne ed be.
Speciﬁcally ,argc will be equal to 1, argv[0] will be the string “./a.out”,
and argv[1] will be null, indicating the end of the array .
F.3 Useful Flags
Before moving on to the C language, we’ll ﬁrst point out some useful
compilation ﬂags for gcc.
prompt> gcc -o hw hw.c # -o: to specify the executable name
prompt> gcc -Wall hw.c # -Wall: gives much better warnings
prompt> gcc -g hw.c # -g: to enable debugging with gdb
prompt> gcc -O hw.c # -O: to turn on optimization
Of course, you may combine these ﬂags as you see ﬁt (e.g., gcc -o
hw -g -Wall hw.c ). Of these ﬂags, you should always use -Wall,
which gives you lots of extra warnings about possible mistakes. Don’t
ignore the warnings! Instead, ﬁx them and thus make them blissfully
disappear.
F.4 Linking with Libraries
Sometimes, you may want to use a library routine in your program.
Because so many routines are available in the C library (which is auto-
matically linked with every program), all you usually have to d o is ﬁnd
the right #include ﬁle. The best way to do that is via the manual pages,
usually just called the man pages.
For example, let’s say you want to use the fork() system call 1. By
typing man fork at the shell prompt, you will get back a text description
of how fork() works. At the very top will be a short code snippet, and
that will tell you which ﬁles you need to #include in your program in
order to get it to compile. In the case of fork(), you need to #include
the ﬁle unistd.h, which would be accomplished as follows:
1Note that fork() is a system call, and not just a library routine. However, the C libr ary
provides C wrappers for all the system calls, each of which simply tr ap into the operating
system.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

4 L ABORATORY : T UTORIAL
#include <unistd.h>
However, some library routines do not reside in the C library , and
therefore you will have to do a little more work. For example, the ma th
library has many useful routines, such as sines, cosines, tang ents, and the
like. If you want to include the routine tan() in our code, you should
again ﬁrst check the man page. At the top of the Linux man page for t an,
you will see the following two lines:
#include <math.h>
...
Link with -lm.
The ﬁrst line you already should understand — you need to#include
the math library , which is found in the standard location in the ﬁle system
(i.e., /usr/include/math.h). However, what the next line is telling
you is how to “link” your program with the math library . A number
of useful libraries exist and can be linked with; many of those re side in
/usr/lib; it is indeed where the math library is found.
There are two types of libraries: statically-linked librari es (which end
in .a), and dynamically-linked ones (which end in .so). Statically-linked
libraries are combined directly into your executable; that is , the low-level
code for the library is inserted into your executable by the link er, and re-
sults in a much larger binary object. Dynamic linking improves on this
by just including the reference to a library in your program exe cutable;
when the program is run, the operating system loader dynamicall y links
in the library . This method is preferred over the static approac h because
it saves disk space (no unnecessarily large executables are made) and al-
lows applications to share library code and static data in memory . In the
case of the math library , both static and dynamic versions are av ailable,
with the static version called /usr/lib/libm.a and the dynamic one
/usr/lib/libm.so.
In any case, to link with the math library , you need to specify t he li-
brary to the link-editor; this can be achieved by invoking gcc with the
right ﬂags.
prompt> gcc -o hw hw.c -Wall -lm
The -lXXX ﬂag tells the linker to look for libXXX.so or libXXX.a,
probably in that order. If for some reason you insist on the static lib rary
over the dynamic one, there is another ﬂag you can use — see if you can
ﬁnd out what it is. People sometimes prefer the static version of a l ibrary
because of the slight performance cost associated with using dyn amic li-
braries.
One ﬁnal note: if you want the compiler to search for headers in a di f-
ferent path than the usual places, or want it to link with libra ries that you
specify , you can use the compiler ﬂag-I/foo/bar to look for headers in
the directory /foo/bar, and the -L/foo/bar ﬂag to look for libraries in
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LABORATORY : T UTORIAL 5
the /foo/bar directory . One common directory to specify in this manner
is “.” (called “dot”), which is U NIX shorthand for the current directory .
Note that the -I ﬂag should go on a compile line, and the -L ﬂag on the
link line.
F.5 Separate Compilation
Once a program starts to get large enough, you may want to split
it into separate ﬁles, compiling each separately , and then li nk them to-
gether. For example, say you have two ﬁles, hw.c and helper.c, and
you wish to compile them individually , and then link them togeth er.
# we are using -Wall for warnings, -O for optimization
prompt> gcc -Wall -O -c hw.c
prompt> gcc -Wall -O -c helper.c
prompt> gcc -o hw hw.o helper.o -lm
The -c ﬂag tells the compiler just to produce an object ﬁle — in this
case, ﬁles called hw.o and helper.o. These ﬁles are not executables,
but just machine-level representations of the code within each source
ﬁle. To combine the object ﬁles into an executable, you have to “l ink”
them together; this is accomplished with the third line gcc -o hw hw.o
helper.o). In this case, gcc sees that the input ﬁles speciﬁed are not
source ﬁles (.c), but instead are object ﬁles ( .o), and therefore skips right
to the last step and invoked the link-editor ld to link them together into a
single executable. Because of its function, this line is often c alled the “link
line”, and would be where you specify link-speciﬁc commands suc h as
-lm. Analogously , ﬂags such as -Wall and -O are only needed in the
compile phase, and therefore need not be included on the link line but
rather only on compile lines.
Of course, you could just specify all the C source ﬁles on a single li ne
to gcc (gcc -Wall -O -o hw hw.c helper.c ), but this requires the
system to recompile every source-code ﬁle, which can be a time-consuming
process. By compiling each individually , you can save time by onl y re-
compiling those ﬁles that have changed during your editing, and thus
increase your productivity . This process is best managed by anot her pro-
gram, make, which we now describe.
F.6 Makeﬁles
The program make lets you automate much of your build process,
and is thus a crucially important tool for any serious program (and p ro-
grammer). Let’s take a look at a simple example, saved in a ﬁle cal led
Makefile.
To build your program, now all you have to do is type make at the
command line.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

6 L ABORATORY : T UTORIAL
hw: hw.o helper.o
gcc -o hw hw.o helper.o -lm
hw.o: hw.c
gcc -O -Wall -c hw.c
helper.o: helper.c
gcc -O -Wall -c helper.c
clean:
rm -f hw.o helper.o hw
This will (by default) look for Makefile or makefile, and use that
as its input (you can specify a different makeﬁle with a ﬂag; re ad the
man pages to ﬁnd out which). The gnu version of make, gmake, is more
fully featured than traditional make, so we will focus upon it for the rest
of this discussion (though we will use the two terms interchange ably).
Most of these notes are based on the gmake info page; to see how to ﬁnd
those pages, see the Documentation section below. Also note: on Linu x
systems, gmake and make are one and the same.
Makeﬁles are based on rules, which are used to decide what need s to
happen. The general form of a rule:
target: prerequisite1 prerequisite2 ...
command1
command2
...
A target is usually the name of a ﬁle that is generated by a command;
examples of targets are executable or object ﬁles. A target can a lso be the
name of an action to carry out, such as “clean” in our example.
A prerequisite is a ﬁle that is used as input to create the target. A
target often depends on several ﬁles. For example, to build the e xecutable
hw, we need two object ﬁles to be built ﬁrst: hw.o and helper.o.
Finally , acommand is an action that make carries out. A rule may have
more than one command, each on its own line. Important: You have to
put a single tab character at the beginning of every command lin e! If you
just put spaces, make will print out some obscure error message and exit.
Usually a command is in a rule with prerequisites and serves to cre-
ate a target ﬁle if any of the prerequisites change. However, th e rule that
speciﬁes commands for the target need not have prerequisites. F or ex-
ample, the rule containing the delete command associated with t he target
“clean” does not have prerequisites.
Going back to our example, when make is executed, it roughly works
like this: First, it comes to the target hw, and it realizes that to build it, it
must have two prerequisites, hw.o and helper.o. Thus, hw depends on
those two object ﬁles. Make then will examine each of those target s. In
examining hw.o, it will see that it depends on hw.c. Here is the key: if
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LABORATORY : T UTORIAL 7
hw.c has been modiﬁed more recently than hw.o has been created, make
will know that hw.o is out of date and should be generated anew; in that
case, it will execute the command line, gcc -O -Wall -c hw.c , which
generates hw.o. Thus, if you are compiling a large program, make will
know which object ﬁles need to be re-generated based on their dep en-
dencies, and will only do the necessary amount of work to recreate the
executable. Also note that hw.o will be created in the case that it does
not exist at all.
Continuing along, helper.o may also be regenerated or created, based
on the same criteria as deﬁned above. When both of the object ﬁles
have been created, make is now ready to execute the command to cr e-
ate the ﬁnal executable, and goes back and does so: gcc -o hw hw.o
helper.o -lm .
Up until now, we’ve been ignoring the clean target in the makeﬁle.
To use it, you have to ask for it explicitly . Type
prompt> make clean
This will execute the command on the command line. Because there
are no prerequisites for the clean target, typing make clean will al-
ways result in the command(s) being executed. In this case, th e clean
target is used to remove the object ﬁles and executable, quite h andy if
you wish to rebuild the entire program from scratch.
Now you might be thinking, “well, this seems OK, but these makeﬁ les
sure are cumbersome!” And you’d be right — if they always had to be
written like this. Fortunately , there are a lot of shortcuts that make make
even easier to use. For example, this makeﬁle has the same func tionality
but is a little nicer to use:
# specify all source files here
SRCS = hw.c helper.c
# specify target here (name of executable)
TARG = hw
# specify compiler, compile flags, and needed libs
CC = gcc
OPTS = -Wall -O
LIBS = -lm
# this translates .c files in src list to .o’s
OBJS = $(SRCS:.c=.o)
# all is not really needed, but is used to generate the target
all: $(TARG)
# this generates the target executable
$(TARG): $(OBJS)
$(CC) -o $(TARG) $(OBJS) $(LIBS)
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

8 L ABORATORY : T UTORIAL
# this is a generic rule for .o files
%.o: %.c
$(CC) $(OPTS) -c $< -o $@
# and finally, a clean line
clean:
rm -f $(OBJS) $(TARG)
Though we won’t go into the details of make syntax, as you can see,
this makeﬁle can make your life somewhat easier. For example, it allows
you to easily add new source ﬁles into your build, simply by adding them
to the SRCS variable at the top of the makeﬁle. You can also easily change
the name of the executable by changing the TARG line, and the compiler,
ﬂags, and library speciﬁcations are all easily modiﬁed.
One ﬁnal word about make: ﬁguring out a target’s prerequisites is not
always trivial, especially in large and complex programs. Not s urpris-
ingly , there is another tool that helps with this, calledmakedepend. Read
about it on your own and see if you can incorporate it into a makeﬁle.
F.7 Debugging
Finally , after you have created a good build environment, and a cor -
rectly compiled program, you may ﬁnd that your program is buggy . On e
way to ﬁx the problem(s) is to think really hard — this method is s ome-
times successful, but often not. The problem is a lack of information; you
just don’t know exactly what is going on within the program, and ther e-
fore cannot ﬁgure out why it is not behaving as expected. Fortunate ly ,
there is some help: gdb, the GNU debugger.
Let’s take the following buggy code, saved in the ﬁle buggy.c, and
compiled into the executable buggy.
#include <stdio.h>
struct Data {
int x;
};
int
main(int argc, char *argv[])
{
struct Data *p = NULL;
printf("%d\n", p->x);
}
In this example, the main program dereferences the variable p when
it is NULL, which will lead to a segmentation fault. Of course, t his prob-
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LABORATORY : T UTORIAL 9
lem should be easy to ﬁx by inspection, but in a more complex program ,
ﬁnding such a problem is not always easy .
To prepare yourself for a debugging session, recompile your progra m
and make sure to pass the -g ﬂag to each compile line. This includes extra
debugging information in your executable that will be useful during your
debugging session. Also, don’t turn on optimization ( -O); though this
may work, it may also lead to confusion during debugging.
After re-compiling with -g, you are ready to use the debugger. Fire
up gdb at the command prompt as follows:
prompt> gdb buggy
This puts you inside an interactive session with the debugger. Note
that you can also use the debugger to examine “core” ﬁles that we re pro-
duced during bad runs, or to attach to an already-running progr am; read
the documentation to learn more about this.
Once inside, you may see something like this:
prompt> gdb buggy
GNU gdb ...
Copyright 2008 Free Software Foundation, Inc.
(gdb)
The ﬁrst thing you might want to do is to go ahead and run the pro-
gram. To do this, simply type run at gdb command prompt. In this case,
this is what you might see:
(gdb) run
Starting program: buggy
Program received signal SIGSEGV, Segmentation fault.
0x8048433 in main (argc=1, argv=0xbffff844) at buggy.c:19
19 printf("%d\n", p->x);
As you can see from the example, in this case, gdb immediately pin-
points where the problem occurred; a “segmentation fault” was ge ner-
ated at the line where we tried to dereference p. This just means that we
accessed some memory that we weren’t supposed to access. At this p oint,
the astute programmer can examine the code, and say “aha! it mus t be
that p does not point to anything valid, and thus should not be derefer-
enced!”, and then go ahead and ﬁx the problem.
However, if you didn’t know what was going on, you might want to
examine some variable. gdb allows you to do this interactively during
the debug session.
(gdb) print p
1 = (Data *) 0x0
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

10 L ABORATORY : T UTORIAL
By using the print primitive, we can examine p, and see both that it is
a pointer to a struct of type Data, and that it is currently set to NULL (or
zero, or hex zero which is shown here as “0x0”).
Finally , you can also set breakpoints within your program to have the
debugger stop the program at a certain routine. After doing this, it is
often useful to step through the execution (one line at a time), an d see
what is happening.
(gdb) break main
Breakpoint 1 at 0x8048426: file buggy.c, line 17.
(gdb) run
Starting program: /homes/hacker/buggy
Breakpoint 1, main (argc=1, argv=0xbffff844) at buggy.c:1 7
17 struct Data *p = NULL;
(gdb) next
19 printf("%d\n", p->x);
(gdb) next
Program received signal SIGSEGV, Segmentation fault.
0x8048433 in main (argc=1, argv=0xbffff844) at buggy.c:19
19 printf("%d\n", p->x);
In the example above, a breakpoint is set at the main() routine; thus,
when we run the program, the debugger almost immediately stops e xe-
cution at main. At that point in the example, a “next” command is i ssued,
which executes the next source-level command. Both “next” and “ step”
are useful ways to advance through a program — read about them in t he
documentation for more details 2.
This discussion really does not do gdb justice; it is a rich and ﬂexi-
ble debugging tool, with many more features than can be describe d in
the limited space here. Read more about it on your own and become an
expert in your copious spare time.
F.8 Documentation
To learn a lot more about all of these things, you have to do two things:
the ﬁrst is to use these tools, and the second is to read more about th em
on your own. One way to ﬁnd out more about gcc, gmake, and gdb is to
read their man pages; type man gcc , man gmake , or man gdb at your
command prompt. You can also use man -k to search the man pages for
keywords, though that doesn’t always work as well as it might; googli ng
is probably a better approach here.
One tricky thing about man pages: typing man XXX may not result
in the thing you want, if there is more than one thing called XXX. For
2In particular, you can use the interactive “help” command while debugg ing with gdb
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LABORATORY : T UTORIAL 11
example, if you are looking for the kill() system call man page, and
if you just type man kill at the prompt, you will get the wrong man
page, because there is a command-line program called kill. Man pages
are divided into sections, and by default, man will return the man page
in the lowest section that it ﬁnds, which in this case is section 1 . Note that
you can tell which man page you got by looking at the top of the page:
if you see kill(2), you know you are in the right man page in Section
2, where system calls live. Type man man to learn more about what is
stored in each of the different sections of the man pages. Also note that
man -a kill can be used to cycle through all of the different man pages
named “kill”.
Man pages are useful for ﬁnding out a number of things. In particu lar,
you will often want to look up what arguments to pass to a library ca ll,
or what header ﬁles need to be included to use a library call. Al l of this
should be available in the man page. For example, if you look up the
open() system call, you will see:
SYNOPSIS
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
int open(const char *path, int oflag, / * mode_t mode */...);
That tells you to include the headers sys/types.h, sys/stat.h,
and fcntl.h in order to use the open call. It also tells you about the
parameters to pass to open, namely a string called path, and integer ﬂag
oflag, and an optional argument to specify the mode of the ﬁle. If there
were any libraries you needed to link with to use the call, it wou ld tell
you that here too.
Man pages require some effort to use effectively . They are often di-
vided into a number of standard sections. The main body will desc ribe
how you can pass different parameters in order to have the functi on be-
have differently .
One particularly useful section is called the RETURN VALUES part of
the man page, and it tells you what the function will return unde r success
or failure. From the open() man page again:
RETURN VALUES
Upon successful completion, the open() function opens the
file and return a non-negative integer representing the
lowest numbered unused file descriptor. Otherwise, -1 is
returned, errno is set to indicate the error, and no files
are created or modified.
Thus, by checking what open returns, you can see if the open suc-
ceeded or not. If it didn’t, open (and many standard library routin es) will
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

12 L ABORATORY : T UTORIAL
set a global variable called errno to a value to tell you about the error.
See the ERRORS section of the man page for more details.
Another thing you might want to do is to look for the deﬁnition of a
structure that is not speciﬁed in the man page itself. For examp le, the
man page for gettimeofday() has the following synopsis:
SYNOPSIS
#include <sys/time.h>
int gettimeofday(struct timeval *restrict tp,
void *restrict tzp);
From this page, you can see that the time is put into a structure of
type timeval, but the man page may not tell you what ﬁelds that struct
has! (in this case, it does, but you may not always be so lucky) Thu s, you
may have to hunt for it. All include ﬁles are found under the dire ctory
/usr/include, and thus you can use a tool like grep to look for it. For
example, you might type:
prompt> grep ’struct timeval’ /usr/include/sys/ *.h
This lets you look for the deﬁnition of the structure in all ﬁles that
end with .h in /usr/include/sys. Unfortunately , this may not always
work, as that include ﬁle may include others which are found else where.
A better way to do this is to use a tool at your disposal, the com-
piler. Write a program that includes the header time.h, let’s say called
main.c. Then, instead of compiling it, use the compiler to invoke the
preprocessor. The preprocessor processes all the directives in y our ﬁle,
such as #define commands and #include commands. To do this, type
gcc -E main.c . The result of this is a C ﬁle that has all of the needed
structures and prototypes in it, including the deﬁnition of the t imeval
struct.
Probably an even better way to ﬁnd these things out: google. You
should always google things you don’t know about — it’s amazing how
much you can learn simply by looking it up!
Info Pages
Also quite useful in the hunt for documentation are the info pages, which
provide much more detailed documentation on many GNU tools. You
can access the info pages by running the program info, or via emacs,
the preferred editor of hackers, by executing Meta-x info . A program
like gcc has hundreds of ﬂags, and some of them are surprisingly useful
to know about. gmake has many more features that will improve your
build environment. Finally , gdb is quite a sophisticated debugger. Read
the man and info pages, try out features that you hadn’t tried bef ore, and
become a power user of your programming tools.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

LABORATORY : T UTORIAL 13
F.9 Suggested Readings
Other than the man and info pages, there are a number of useful b ooks
out there. Note that a lot of this information is available for free on- line;
however, sometimes having something in book form seems to make it
easier to learn. Also, always look for O’Reilly books on topics you are
interested in; they are almost always of high quality .
• “The C Programming Language”, by Brian Kernighan and Dennis
Ritchie. This is the deﬁnitive C book to have.
• “Managing Projects with make”, by Andrew Oram and Steve Tal-
bott. A reasonable and short book on make.
• “Debugging with GDB: The GNU Source-Level Debugger”, by Rich ard
M. Stallman, Roland H. Pesch. A little book on using GDB.
• “Advanced Programming in the UNIX Environment”, by W. Richard
Stevens and Steve Rago. Stevens wrote some excellent books, and
this is a must for UNIX hackers. He also has an excellent set of books
on TCP/IP and Sockets programming.
• “Expert C Programming”, by Peter Van der Linden. A lot of the
useful tips about compilers, etc., above are stolen directly from here.
Read this! It is a great and eye-opening book, even though a little
out of date.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES
