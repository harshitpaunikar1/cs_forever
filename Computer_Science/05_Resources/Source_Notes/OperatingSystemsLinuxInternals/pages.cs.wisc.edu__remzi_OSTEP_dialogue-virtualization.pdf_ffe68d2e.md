Title: dialogue-virtualization.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/dialogue-virtualization.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:08+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

Part I
Virtualization
1

3
A Dialogue on Virtualization
Professor: And thus we reach the ﬁrst of our three pieces on operating system s:
virtualization.
Student: But what is virtualization, oh noble professor?
Professor: Imagine we have a peach.
Student: A peach? (incredulous)
Professor: Y es, a peach. Let us call that the physical peach. But we have many
eaters who would like to eat this peach. What we would like to present t o each
eater is their own peach, so that they can be happy. We call the pea ch we give
eaters virtual peaches; we somehow create many of these virtual peaches out o f
the one physical peach. And the important thing: in this illusion, it look s to each
eater like they have a physical peach, but in reality they don’t.
Student: So you are sharing the peach, but you don’t even know it?
Professor: Right! Exactly.
Student: But there’s only one peach.
Professor: Y es. And...?
Student: Well, if I was sharing a peach with somebody else, I think I would
notice.
Professor: Ah yes! Good point. But that is the thing with many eaters; most
of the time they are napping or doing something else, and thus, you c an snatch
that peach away and give it to someone else for a while. And thus we cre ate the
illusion of many virtual peaches, one peach for each person!
Student: Sounds like a bad campaign slogan. Y ou are talking about computers,
right Professor?
Professor: Ah, young grasshopper, you wish to have a more concrete example .
Good idea! Let us take the most basic of resources, the CPU. Assu me there is one
physical CPU in a system (though now there are often two or four or more). What
virtualization does is take that single CPU and make it look like many virtu al
CPUs to the applications running on the system. Thus, while each app lication
3

4 A D IALOGUE ON VIRTUALIZATION
thinks it has its own CPU to use, there is really only one. And thus the O S has
created a beautiful illusion: it has virtualized the CPU.
Student: Wow! That sounds like magic. T ell me more! How does that work?
Professor: In time, young student, in good time. Sounds like you are ready to
begin.
Student: I am! Well, sort of. I must admit, I’m a little worried you are going to
start talking about peaches again.
Professor: Don’t worry too much; I don’t even like peaches. And thus we be-
gin...
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
