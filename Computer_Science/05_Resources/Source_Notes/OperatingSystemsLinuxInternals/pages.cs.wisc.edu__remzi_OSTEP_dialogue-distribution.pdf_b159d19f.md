Title: dialogue-distribution.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/dialogue-distribution.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:02+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

47
A Dialogue on Distribution
Professor: And thus we reach our ﬁnal little piece in the world of operating
systems: distributed systems. Since we can’t cover much here, w e’ll sneak in a
little intro here in the section on persistence, and focus mostly on dist ributed ﬁle
systems. Hope that is OK!
Student: Sounds OK. But what is a distributed system exactly, oh glorious and
all-knowing professor?
Professor: Well, I bet you know how this is going to go...
Student: There’s a peach?
Professor: Exactly! But this time, it’s far away from you, and may take some
time to get the peach. And there are a lot of them! Even worse, som etimes a
peach becomes rotten. But you want to make sure that when anyb ody bites into
a peach, they will get a mouthful of deliciousness.
Student: This peach analogy is working less and less for me.
Professor: Come on! It’s the last one, just go with it.
Student: Fine.
Professor: So anyhow, forget about the peaches. Building distributed systems
is hard, because things fail all the time. Messages get lost, machines go down,
disks corrupt data. It’s like the whole world is working against you!
Student: But I use distributed systems all the time, right?
Professor: Y es! Y ou do. And... ?
Student: Well, it seems like they mostly work. After all, when I send a search
request to Google, it usually comes back in a snap, with some great re sults! Same
thing when I use Facebook, Amazon, and so forth.
1

2 A D IALOGUE ON DISTRIBUTION
Professor: Y es, it is amazing. And that’s despite all of those failures taking
place! Those companies build a huge amount of machinery into their sy stems so
as to ensure that even though some machines have failed, the entire system stays
up and running. They use a lot of techniques to do this: replication, r etry, and
various other tricks people have developed over time to detect and recover from
failures.
Student: Sounds interesting. Time to learn something for real?
Professor: It does seem so. Let’s get to work! But ﬁrst things ﬁrst ...
(bites into peach he has been holding, which unfortunately is rotten)
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
