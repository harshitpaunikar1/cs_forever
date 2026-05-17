Title: dialogue-threeeasy.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/dialogue-threeeasy.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:07+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

1
A Dialogue on the Book
Professor: Welcome to this book! It’s called Operating Systems in Three Easy
Pieces, and I am here to teach you the things you need to know about oper ating
systems. I am called “Professor”; who are you?
Student: Hi Professor! I am called “Student”, as you might have guessed. An d
I am here and ready to learn!
Professor: Sounds good. Any questions?
Student: Sure! Why is it called “Three Easy Pieces”?
Professor: That’s an easy one. Well, you see, there are these great lectures on
Physics by Richard Feynman...
Student: Oh! The guy who wrote “Surely Y ou’re Joking, Mr. Feynman”, right?
Great book! Is this going to be hilarious like that book was?
Professor: Um... well, no. That book was great, and I’m glad you’ve read it.
Hopefully this book is more like his notes on Physics. Some of the basics w ere
summed up in a book called “Six Easy Pieces”. He was talking about Phys ics;
we’re going to do Three Easy Pieces on the ﬁne topic of Operating Syst ems. This
is appropriate, as Operating Systems are about half as hard as Phy sics.
Student: Well, I liked physics, so that is probably good. What are those pieces?
Professor: They are the three key ideas we’re going to learn about: virtualiza-
tion, concurrency, and persistence. In learning about these ideas, we’ll learn
all about how an operating system works, including how it decides what program
to run next on a CPU, how it handles memory overload in a virtual memo ry sys-
tem, how virtual machine monitors work, how to manage information o n disks,
and even a little about how to build a distributed system that works wh en parts
have failed. That sort of stuff.
Student: I have no idea what you’re talking about, really.
Professor: Good! That means you are in the right class.
Student: I have another question: what’s the best way to learn this stuff?
1

2 A D IALOGUE ON THE BOOK
Professor: Excellent query! Well, each person needs to ﬁgure this out on their
own, of course, but here is what I would do: go to class, to hear the professor
introduce the material. Then, at the end of every week, read thes e notes, to help
the ideas sink into your head a bit better. Of course, some time later (hint: before
the exam!), read the notes again to ﬁrm up your knowledge. Of cour se, your pro-
fessor will no doubt assign some homeworks and projects, so you sho uld do those;
in particular, doing projects where you write real code to solve real problems is
the best way to put the ideas within these notes into action. As Confu cius said...
Student: Oh, I know! ’I hear and I forget. I see and I remember. I do and I
understand.’ Or something like that.
Professor: (surprised) How did you know what I was going to say?!
Student: It seemed to follow. Also, I am a big fan of Confucius, and an even
bigger fan of Xunzi, who actually is a better source for this quote 1.
Professor: (stunned) Well, I think we are going to get along just ﬁne! Just ﬁne
indeed.
Student: Professor – just one more question, if I may. What are these dialogue s
for? I mean, isn’t this just supposed to be a book? Why not present t he material
directly?
Professor: Ah, good question, good question! Well, I think it is sometimes
useful to pull yourself outside of a narrative and think a bit; these d ialogues are
those times. So you and I are going to work together to make sense of all of these
pretty complex ideas. Are you up for it?
Student: So we have to think? Well, I’m up for that. I mean, what else do I have
to do anyhow? It’s not like I have much of a life outside of this book.
Professor: Me neither, sadly. So let’s get to work!
1According to http://www.barrypopik.com (on, December 19, 2012, entitled “Tell
me and I forget; teach me and I may remember; involve me and I will lear n”) Confucian
philosopher Xunzi said “Not having heard something is not as good as having heard it; having
heard it is not as good as having seen it; having seen it is not as good as knowing it; knowing
it is not as good as putting it into practice.” Later on, the wisdom got attached to Confucius
for some reason. Thanks to Jiao Dong (Rutgers) for telling us!
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
