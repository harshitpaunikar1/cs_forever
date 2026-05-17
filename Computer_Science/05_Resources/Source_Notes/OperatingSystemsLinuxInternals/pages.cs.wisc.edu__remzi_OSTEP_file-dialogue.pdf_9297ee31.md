Title: file-dialogue.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/file-dialogue.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:19+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

46
Summary Dialogue on Persistence
Student: Wow, ﬁle systems seem interesting(!), and yet complicated.
Professor: That’s why my spouse and I do our research in this space.
Student: Hold on. Are you one of the professors who wrote this book? I thoug ht
we were both just fake constructs, used to summarize some main poin ts, and
perhaps add a little levity in the study of operating systems.
Professor: Uh... er... maybe. And none of your business! And who did you
think was writing these things? (sighs) Anyhow, let’s get on with it: w hat did
you learn?
Student: Well, I think I got one of the main points, which is that it is much
harder to manage data for a long time (persistently) than it is to mana ge data
that isn’t persistent (like the stuff in memory). After all, if your mach ines crashes,
memory contents disappear! But the stuff in the ﬁle system needs to live forever.
Professor: Well, as my friend Kevin Hultquist used to say, “Forever is a long
time”; while he was talking about plastic golf tees, it’s especially true fo r the
garbage that is found in most ﬁle systems.
Student: Well, you know what I mean! For a long time at least. And even simple
things, such as updating a persistent storage device, are complicated, because you
have to care what happens if you crash. Recovery, something I ha d never even
thought of when we were virtualizing memory, is now a big deal!
Professor: T oo true. Updates to persistent storage have always been, and r e-
main, a fun and challenging problem.
Student: I also learned about cool things like disk scheduling, and about data
protection techniques like RAID and even checksums. That stuff is c ool.
Professor: I like those topics too. Though, if you really get into it, they can get
a little mathematical. Check out some of the latest on erasure codes if you want
your brain to hurt.
Student: I’ll get right on that.
1

2 S UMMARY DIALOGUE ON PERSISTENCE
Professor: (frowns) I think you’re being sarcastic. Well, what else did you like?
Student: And I also liked all the thought that has gone into building technology-
aware systems, like FFS and LFS. Neat stuff! Being disk aware seems c ool. But
will it matter anymore, with Flash and all the newest, latest technolo gies?
Professor: Good question! Y es, even with Flash, all of this stuff is still relevant,
amazingly. For example, Flash T ranslation Layers (FTLs) use log-st ructuring
internally, to improve performance and reliability of Flash-based SSDs . And
thinking about locality is always useful. So while the technology may be ch ang-
ing, many of the ideas we have studied will continue to be useful, for a wh ile at
least.
Student: That’s good. I just spent all this time learning it, and I didn’t want it
to all be for no reason!
Professor: Professors wouldn’t do that to you, would they?
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
