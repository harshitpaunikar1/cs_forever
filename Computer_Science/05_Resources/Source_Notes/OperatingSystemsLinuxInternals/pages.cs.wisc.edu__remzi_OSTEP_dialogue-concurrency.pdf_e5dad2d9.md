Title: dialogue-concurrency.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/dialogue-concurrency.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:02+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

Part II
Concurrency
1

25
A Dialogue on Concurrency
Professor: And thus we reach the second of our three pillars of operating sys-
tems: concurrency.
Student: I thought there were four pillars...?
Professor: Nope, that was in an older version of the book.
Student: Umm... OK. So what is concurrency, oh wonderful professor?
Professor: Well, imagine we have a peach —
Student: (interrupting) Peaches again! What is it with you and peaches?
Professor: Ever read T.S. Eliot? The Love Song of J. Alfred Prufrock, “Do I dare
to eat a peach”, and all that fun stuff?
Student: Oh yes! In English class in high school. Great stuff! I really liked the
part where —
Professor: (interrupting) This has nothing to do with that — I just like peaches.
Anyhow, imagine there are a lot of peaches on a table, and a lot of peo ple who
wish to eat them. Let’s say we did it this way: each eater ﬁrst identiﬁes a peach
visually, and then tries to grab it and eat it. What is wrong with this app roach?
Student: Hmmm... seems like you might see a peach that somebody else also
sees. If they get there ﬁrst, when you reach out, no peach for you !
Professor: Exactly! So what should we do about it?
Student: Well, probably develop a better way of going about this. Maybe form a
line, and when you get to the front, grab a peach and get on with it.
Professor: Good! But what’s wrong with your approach?
Student: Sheesh, do I have to do all the work?
Professor: Y es.
Student: OK, let me think. Well, we used to have many people grabbing for
peaches all at once, which is faster. But in my way, we just go one at a t ime,
which is correct, but quite a bit slower. The best kind of approach wo uld be fast
and correct, probably.
3

4 A D IALOGUE ON CONCURRENCY
Professor: Y ou are really starting to impress. In fact, you just told us everything
we need to know about concurrency! Well done.
Student: I did? I thought we were just talking about peaches. Remember, this
is usually the part where you make it about computers again.
Professor: Indeed. My apologies! One must never forget the concrete. Well,
as it turns out, there are certain types of programs that we call multi-threaded
applications; each thread is kind of like an independent agent running around
in this program, doing things on the program’s behalf. But these thr eads access
memory, and for them, each spot of memory is kind of like one of those peaches. If
we don’t coordinate access to memory between threads, the pro gram won’t work
as expected. Make sense?
Student: Kind of. But why do we talk about this in an OS class? Isn’t that just
application programming?
Professor: Good question! A few reasons, actually. First, the OS must support
multi-threaded applications with primitives such as locks and condition vari-
ables, which we’ll talk about soon. Second, the OS itself was the ﬁrst concu rrent
program — it must access its own memory very carefully or many stran ge and
terrible things will happen. Really, it can get quite grisly.
Student: I see. Sounds interesting. There are more details, I imagine?
Professor: Indeed there are...
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
