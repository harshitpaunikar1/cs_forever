Title: dialogue-security.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/dialogue-security.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:06+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

52
A Dialogue on Security
Chapter by Peter Reiher (UCLA)
Professor: Hello again, student!
Student: I thought we were done with all this. We’ve already had three pillars,
and I even stuck around for a few appendices. Will I never be done with this
class?
Professor: That depends on who I am. Some professors want to talk about
security and some don’t. Unfortunately for you, given that you’re h ere, I’m one
of those who want to.
Student: OK, I suppose we’d better just get on with it.
Professor: That’s the spirit! Soonest begun, soonest done. So, let’s say yo u
have a peach...
Student: Y ou told me we were at least done with peaches!
Professor: When one is discussing security, lies will always be a part of the
discussion. Anyway, you’ve got a peach. Y ou certainly wouldn’t wan t to turn
around and ﬁnd someone had stolen your peach, would you?
Student: Well, if it isn’t as rotten as the one you ended up with, I suppose not.
Professor: And you probably wouldn’t be any happier if you turned around
and discovered someone had swapped out your peach for a turnip, e ither, would
you?
Student: I guess not, though I do know a couple of good recipes for turnips.
Professor: And you also wouldn’t want somebody slapping your hand away
every time you reached for your peach, right?
Student: No, that would be pretty rude.
Professor: Y ou wouldn’t want that happening to any of the resources your com-
puter controls, either. Y ou might be even unhappier, if they’re rea lly important
resources. Y ou wouldn’t want the love letter you’re in the middle of c omposing
to leak out, you wouldn’t want someone to reset the saved state in your favorite
game to take you back to the very beginning, and you would be mighty upset if,
at midnight the evening before your project was due, you weren’t allo wed to log
into your computer.
1

2 A D IALOGUE ON SECURITY
Student: T rue, those would all pretty much suck.
Professor: Let’s try to keep a professional tone here. After all, this is a class-
room. Kind of. That’s what operating system security is all about, a nd that’s
what I’m here to tell you about. How can you ensure that secrets r emain con-
ﬁdential? How can you guarantee the integrity of your important dat a? How
can you ensure that you can use your computer resources when y ou want to?
And these questions apply to all of the resources in your computer , all the time,
forever.
Student: All this sounds a little like reliability stuff we talked about before...
Professor: Y es and no. Bad things can happen more or less by accident or
through poor planning, and reliability is about those sorts of things. But we’re
going a step further. SOMEBODY WANTS YOUR PEACH!!!!
Student: Stop shouting! Y ou were the one asking for a professional tone.
Professor: My apologies, I get excited about this stuff sometimes. The point
I was trying to make is that when we talk about security, we’re talking about
genuine adversaries, human adversaries who are trying to make th ings go wrong
for you. That has some big implications. They’re likely to be clever, malev olent,
persistent, ﬂexible, and sneaky. Y ou may already feel like the univers e has it in
for you (most students feel that way, at any rate), but these folks really, truly are
out to get you. Y ou’re going to have to protect your assets despit e anything they
try.
Student: This sounds challenging.
Professor: Y ou have no idea... But you will! YOU WILL!! (maniacal laughter)
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
