Title: dist-afs.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/dist-afs.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:12+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

50
The Andrew File System (AFS)
The Andrew File System was introduced at Carnegie-Mellon Unive rsity
(CMU) 1 in the 1980’s [H+88]. Led by the well-known Professor M. Satya-
narayanan of Carnegie-Mellon University (“Satya” for short), th e main
goal of this project was simple: scale. Speciﬁcally , how can one design a
distributed ﬁle system such that a server can support as many c lients as
possible?
Interestingly , there are numerous aspects of design and imple menta-
tion that affect scalability . Most important is the design of theprotocol be-
tween clients and servers. In NFS, for example, the protocol forces clients
to check with the server periodically to determine if cached c ontents have
changed; because each check uses server resources (includin g CPU and
network bandwidth), frequent checks like this will limit the number of
clients a server can respond to and thus limit scalability .
AFS also differs from NFS in that from the beginning, reasonable user-
visible behavior was a ﬁrst-class concern. In NFS, cache consist ency is
hard to describe because it depends directly on low-level impl ementa-
tion details, including client-side cache timeout intervals . In AFS, cache
consistency is simple and readily understood: when the ﬁle is ope ned, a
client will generally receive the latest consistent copy from t he server.
50.1 AFS V ersion 1
We will discuss two versions of AFS [H+88, S+85]. The ﬁrst version
(which we will call AFSv1, but actually the original system was called
the ITC distributed ﬁle system [S+85]) had some of the basic desi gn in
place, but didn’t scale as desired, which led to a re-design an d the ﬁnal
protocol (which we will call AFSv2, or just AFS) [H+88]. We now discus s
the ﬁrst version.
1Though originally referred to as “Carnegie-Mellon University”, CMU l ater dropped
the hyphen, and thus was born the modern form, “Carnegie Mellon Universit y .” As AFS
derived from work in the early 80’s, we refer to CMU in its original fu lly-hyphenated form. See
https://www.quora.com/When-did-Carnegie-Mellon-University-remove-the-
hyphen-in-the-university-name for more details, if you are into really boring minutiae.
1

2 T HE ANDREW FILE SYSTEM (AFS)
TestAuth Test whether a file has changed
(used to validate cached entries)
GetFileStat Get the stat info for a file
Fetch Fetch the contents of file
Store Store this file on the server
SetFileStat Set the stat info for a file
ListDir List the contents of a directory
Figure 50.1: AFSv1 Protocol Highlights
One of the basic tenets of all versions of AFS is whole-ﬁle caching on
the local disk of the client machine that is accessing a ﬁle. When you
open() a ﬁle, the entire ﬁle (if it exists) is fetched from the server a nd
stored in a ﬁle on your local disk. Subsequent application read() and
write() operations are redirected to the local ﬁle system where the ﬁle is
stored; thus, these operations require no network communication and are
fast. Finally , upon close(), the ﬁle (if it has been modiﬁed) is ﬂushed
back to the server. Note the obvious contrasts with NFS, which cach es
blocks (not whole ﬁles, although NFS could of course cache every block of
an entire ﬁle) and does so in client memory (not local disk).
Let’s get into the details a bit more. When a client application ﬁ rst calls
open(), the AFS client-side code (which the AFS designers call V enus)
would send a Fetch protocol message to the server. The Fetch protocol
message would pass the entire pathname of the desired ﬁle (for ex am-
ple, /home/remzi/notes.txt) to the ﬁle server (the group of which
they called Vice), which would then traverse the pathname, ﬁnd the de-
sired ﬁle, and ship the entire ﬁle back to the client. The clie nt-side code
would then cache the ﬁle on the local disk of the client (by writing it to
local disk). As we said above, subsequent read() and write() system
calls are strictly local in AFS (no communication with the server occurs);
they are just redirected to the local copy of the ﬁle. Because the read()
and write() calls act just like calls to a local ﬁle system, once a block
is accessed, it also may be cached in client memory . Thus, AFS a lso uses
client memory to cache copies of blocks that it has in its local disk . Fi-
nally , when ﬁnished, the AFS client checks if the ﬁle has been modiﬁed
(i.e., that it has been opened for writing); if so, it ﬂushes the n ew version
back to the server with a Store protocol message, sending the entir e ﬁle
and pathname to the server for permanent storage.
The next time the ﬁle is accessed, AFSv1 does so much more efﬁ-
ciently . Speciﬁcally , the client-side code ﬁrst contacts the s erver (using
the TestAuth protocol message) in order to determine whether the ﬁle
has changed. If not, the client would use the locally-cached copy , thus
improving performance by avoiding a network transfer. The ﬁgure above
shows some of the protocol messages in AFSv1. Note that this early ver-
sion of the protocol only cached ﬁle contents; directories, for exampl e,
were only kept at the server.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

THE ANDREW FILE SYSTEM (AFS) 3
TIP : M EASURE THEN BUILD (PATTERSON ’ S LAW)
One of our advisors, David Patterson (of RISC and RAID fame), used to
always encourage us to measure a system and demonstrate a proble m
before building a new system to ﬁx said problem. By using experimen-
tal evidence, rather than gut instinct, you can turn the proces s of system
building into a more scientiﬁc endeavor. Doing so also has the fr inge ben-
eﬁt of making you think about how exactly to measure the system bef ore
your improved version is developed. When you do ﬁnally get around to
building the new system, two things are better as a result: ﬁr st, you have
evidence that shows you are solving a real problem; second, you now
have a way to measure your new system in place, to show that it act ually
improves upon the state of the art. And thus we call this Patterson’s Law .
50.2 Problems with V ersion 1
A few key problems with this ﬁrst version of AFS motivated the de-
signers to rethink their ﬁle system. To study the problems in d etail, the
designers of AFS spent a great deal of time measuring their exis ting pro-
totype to ﬁnd what was wrong. Such experimentation is a good thing,
because measurement is the key to understanding how systems work
and how to improve them; obtaining concrete, good data is thus a nece s-
sary part of systems construction. In their study , the authors fou nd two
main problems with AFSv1:
• Path-traversal costs are too high: When performing a Fetch or Store
protocol request, the client passes the entire pathname (e.g.,/home/
remzi/notes.txt) to the server. The server, in order to access the
ﬁle, must perform a full pathname traversal, ﬁrst looking in the root
directory to ﬁnd home, then in home to ﬁnd remzi, and so forth,
all the way down the path until ﬁnally the desired ﬁle is located .
With many clients accessing the server at once, the designers of AFS
found that the server was spending much of its CPU time simply
walking down directory paths.
• The client issues too many T estAuth protocol messages : Much
like NFS and its overabundance of GETATTR protocol messages,
AFSv1 generated a large amount of trafﬁc to check whether a lo-
cal ﬁle (or its stat information) was valid with the TestAuth prot o-
col message. Thus, servers spent much of their time telling cli ents
whether it was OK to use their cached copies of a ﬁle. Most of the
time, the answer was that the ﬁle had not changed.
There were actually two other problems with AFSv1: load was not
balanced across servers, and the server used a single distinc t process per
client thus inducing context switching and other overheads. Th e load
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

4 T HE ANDREW FILE SYSTEM (AFS)
imbalance problem was solved by introducing volumes, which an ad-
ministrator could move across servers to balance load; the context -switch
problem was solved in AFSv2 by building the server with threads i nstead
of processes. However, for the sake of space, we focus here on the main
two protocol problems above that limited the scale of the system.
50.3 Improving the Protocol
The two problems above limited the scalability of AFS; the server CPU
became the bottleneck of the system, and each server could only se r-
vice 20 clients without becoming overloaded. Servers were receiv ing too
many TestAuth messages, and when they received Fetch or Store me s-
sages, were spending too much time traversing the directory hi erarchy .
Thus, the AFS designers were faced with a problem:
THE CRUX : H OW TO DESIGN A S CALABLE FILE PROTOCOL
How should one redesign the protocol to minimize the number of
server interactions, i.e., how could they reduce the number of Te stAuth
messages? Further, how could they design the protocol to make thes e
server interactions efﬁcient? By attacking both of these issue s, a new pro-
tocol would result in a much more scalable version AFS.
50.4 AFS V ersion 2
AFSv2 introduced the notion of a callback to reduce the number of
client/server interactions. A callback is simply a promise fr om the server
to the client that the server will inform the client when a ﬁle t hat the
client is caching has been modiﬁed. By adding this state to the system,
the client no longer needs to contact the server to ﬁnd out if a cac hed ﬁle
is still valid. Rather, it assumes that the ﬁle is valid until the server tells it
otherwise; notice the analogy to polling versus interrupts.
AFSv2 also introduced the notion of a ﬁle identiﬁer (FID) (similar to
the NFS ﬁle handle ) instead of pathnames to specify which ﬁle a client
was interested in. An FID in AFS consists of a volume identiﬁer, a ﬁle
identiﬁer, and a “uniquiﬁer” (to enable reuse of the volume and ﬁle IDs
when a ﬁle is deleted). Thus, instead of sending whole pathname s to
the server and letting the server walk the pathname to ﬁnd the desired
ﬁle, the client would walk the pathname, one piece at a time, cac hing the
results and thus hopefully reducing the load on the server.
For example, if a client accessed the ﬁle /home/remzi/notes.txt,
and home was the AFS directory mounted onto / (i.e., / was the local root
directory , but home and its children were in AFS), the client would ﬁrst
Fetch the directory contents of home, put them in the local-disk cache,
and set up a callback on home. Then, the client would Fetch the directory
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

THE ANDREW FILE SYSTEM (AFS) 5
Client (C1) Server
fd = open(“/home/remzi/notes.txt”, ...);
Send Fetch (home FID, “remzi”)
Receive Fetch request
look for remzi in home dir
setup callback(C1) on remzi
return remzi’s content/FID
Receive Fetch reply
write remzi to local disk cache
record callback status of remzi
Send Fetch (remzi FID, “notes.txt”)
Receive Fetch request
look for notes.txt in remzi dir
setup callback(C1) on notes.txt
return notes.txt’s content/FID
Receive Fetch reply
write notes.txt to local disk cache
record callback status of notes.txt
local open() of cached notes.txt
return ﬁle descriptor to application
read(fd, buffer, MAX);
perform local read() on cached copy
close(fd);
do local close() on cached copy
if ﬁle has changed, ﬂush to server
fd = open(“/home/remzi/notes.txt”, ...);
Foreach dir (home, remzi)
if (callback(dir) == V ALID)
use local copy for lookup(dir)
else
Fetch (as above)
if (callback(notes.txt) == V ALID)
open local cached copy
return ﬁle descriptor to it
else
Fetch (as above) then open and return fd
Figure 50.2: Reading A File: Client-side And File Server Actions
remzi, put it in the local-disk cache, and set up a callback on remzi.
Finally , the client would Fetch notes.txt, cache this regular ﬁle in the
local disk, set up a callback, and ﬁnally return a ﬁle descript or to the
calling application. See Figure 50.2 for a summary .
The key difference, however, from NFS, is that with each fetch of a
directory or ﬁle, the AFS client would establish a callback with the server,
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

6 T HE ANDREW FILE SYSTEM (AFS)
ASIDE : C ACHE CONSISTENCY IS NOT A PANACEA
When discussing distributed ﬁle systems, much is made of the c ache con-
sistency the ﬁle systems provide. However, this baseline consistency does
not solve all problems with regards to ﬁle access from multiple cl ients.
For example, if you are building a code repository , with multiple c lients
performing check-ins and check-outs of code, you can’t simply rely on
the underlying ﬁle system to do all of the work for you; rather, you h ave
to use explicit ﬁle-level locking in order to ensure that the “right” thing
happens when such concurrent accesses take place. Indeed, an y applica-
tion that truly cares about concurrent updates will add extra ma chinery
to handle conﬂicts. The baseline consistency described in thi s chapter and
the previous one are useful primarily for casual usage, i.e., wh en a user
logs into a different client, they expect some reasonable versi on of their
ﬁles to show up there. Expecting more from these protocols is settin g
yourself up for failure, disappointment, and tear-ﬁlled frust ration.
thus ensuring that the server would notify the client of a change in its
cached state. The beneﬁt is obvious: although the ﬁrst access to /home/
remzi/notes.txt generates many client-server messages (as described
above), it also establishes callbacks for all the directories a s well as the
ﬁle notes.txt, and thus subsequent accesses are entirely loca l and require
no server interaction at all. Thus, in the common case where a ﬁle is
cached at the client, AFS behaves nearly identically to a loca l disk-based
ﬁle system. If one accesses a ﬁle more than once, the second access should
be just as fast as accessing a ﬁle locally .
50.5 Cache Consistency
When we discussed NFS, there were two aspects of cache consisten cy
we considered: update visibility and cache staleness. With update visi-
bility , the question is: when will the server be updated with anew version
of a ﬁle? With cache staleness, the question is: once the server h as a new
version, how long before clients see the new version instead of an old er
cached copy?
Because of callbacks and whole-ﬁle caching, the cache consistency pro-
vided by AFS is easy to describe and understand. There are two im-
portant cases to consider: consistency between processes on different ma-
chines, and consistency between processes on the same machine.
Between different machines, AFS makes updates visible at th e server
and invalidates cached copies at the exact same time, which is when the
updated ﬁle is closed. A client opens a ﬁle, and then writes to it (perhaps
repeatedly). When it is ﬁnally closed, the new ﬁle is ﬂushed to the server
(and thus visible). At this point, the server then “breaks” ca llbacks for
any clients with cached copies; the break is accomplished by con tacting
each client and informing it that the callback it has on the ﬁle i s no longer
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

THE ANDREW FILE SYSTEM (AFS) 7
Client1 Client2 Server Comments
P1 P2 Cache P 3 Cache Disk
open(F) - - - File created
write(A) A - -
close() A - A
open(F) A - A
read() → A A - A
close() A - A
open(F) A - A
write(B) B - A
open(F) B - A Local processes
read() → B B - A see writes immediately
close() B - A
B open(F) A A Remote processes
B read() → A A A do not see writes...
B close() A A
close() B ✚A B ... until close()
B open(F) B B has taken place
B read() → B B B
B close() B B
B open(F) B B
open(F) B B B
write(D) D B B
D write(C) C B
D close() C C
close() D ✁C D
D open(F) D D Unfortunately for P 3
D read() → D D D the last writer wins
D close() D D
Figure 50.3: Cache Consistency Timeline
valid. This step ensures that clients will no longer read stal e copies of
the ﬁle; subsequent opens on those clients will require a re-fet ch of the
new version of the ﬁle from the server (and will also serve to rees tablish
a callback on the new version of the ﬁle).
AFS makes an exception to this simple model between processes on
the same machine. In this case, writes to a ﬁle are immediatel y visible to
other local processes (i.e., a process does not have to wait until a ﬁ le is
closed to see its latest updates). This makes using a single ma chine be-
have exactly as you would expect, as this behavior is based upon ty pical
UNIX semantics. Only when switching to a different machine would y ou
be able to detect the more general AFS consistency mechanism.
There is one interesting cross-machine case that is worthy of fur ther
discussion. Speciﬁcally , in the rare case that processes on diff erent ma-
chines are modifying a ﬁle at the same time, AFS naturally empl oys what
is known as a last writer wins approach (which perhaps should be called
last closer wins ). Speciﬁcally , whichever client calls close() last will
update the entire ﬁle on the server last and thus will be the “wi nning”
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

8 T HE ANDREW FILE SYSTEM (AFS)
ﬁle, i.e., the ﬁle that remains on the server for others to see. Th e result is
a ﬁle that was generated in its entirety either by one client or t he other.
Note the difference from a block-based protocol like NFS: in NFS, writ es
of individual blocks may be ﬂushed out to the server as each clien t is up-
dating the ﬁle, and thus the ﬁnal ﬁle on the server could end up as a mix
of updates from both clients. In many cases, such a mixed ﬁle outpu t
would not make much sense, i.e., imagine a JPEG image getting mod i-
ﬁed by two clients in pieces; the resulting mix of writes would n ot likely
constitute a valid JPEG.
A timeline showing a few of these different scenarios can be seen in
Figure 50.3. The columns show the behavior of two processes (P 1 and P2)
on Client 1 and its cache state, one process (P 3) on Client 2 and its cache
state, and the server (Server), all operating on a single ﬁle cal led, imag-
inatively ,F. For the server, the ﬁgure simply shows the contents of the
ﬁle after the operation on the left has completed. Read through it a nd see
if you can understand why each read returns the results that it does. A
commentary ﬁeld on the right will help you if you get stuck.
50.6 Crash Recovery
From the description above, you might sense that crash recovery is
more involved than with NFS. You would be right. For example, imagin e
there is a short period of time where a server (S) is not able to contac t
a client (C1), for example, while the client C1 is rebooting. Whi le C1
is not available, S may have tried to send it one or more callback re call
messages; for example, imagine C1 had ﬁle F cached on its local di sk, and
then C2 (another client) updated F, thus causing S to send mess ages to all
clients caching the ﬁle to remove it from their local caches. Bec ause C1
may miss those critical messages when it is rebooting, upon rejoin ing the
system, C1 should treat all of its cache contents as suspect. Thu s, upon
the next access to ﬁle F, C1 should ﬁrst ask the server (with a Te stAuth
protocol message) whether its cached copy of ﬁle F is still valid; i f so, C1
can use it; if not, C1 should fetch the newer version from the serve r.
Server recovery after a crash is also more complicated. The proble m
that arises is that callbacks are kept in memory; thus, when a s erver re-
boots, it has no idea which client machine has which ﬁles. Thus, upon
server restart, each client of the server must realize that th e server has
crashed and treat all of their cache contents as suspect, and (a s above)
reestablish the validity of a ﬁle before using it. Thus, a serve r crash is a
big event, as one must ensure that each client is aware of the cra sh in a
timely manner, or risk a client accessing a stale ﬁle. There ar e many ways
to implement such recovery; for example, by having the server s end a
message (saying “don’t trust your cache contents!”) to each clien t when
it is up and running again, or by having clients check that the s erver is
alive periodically (with a heartbeat message, as it is called). As you can
see, there is a cost to building a more scalable and sensible caching model;
with NFS, clients hardly noticed a server crash.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

THE ANDREW FILE SYSTEM (AFS) 9
AFS
Workload NFS AFS NFS
1. Small ﬁle, sequential read Ns · Lnet Ns · Lnet 1
2. Small ﬁle, sequential re-read Ns · Lmem Ns · Lmem 1
3. Medium ﬁle, sequential read Nm · Lnet Nm · Lnet 1
4. Medium ﬁle, sequential re-read Nm · Lmem Nm · Lmem 1
5. Large ﬁle, sequential read NL · Lnet NL · Lnet 1
6. Large ﬁle, sequential re-read NL · Lnet NL · Ldisk
Ldisk
Lnet
7. Large ﬁle, single read Lnet NL · Lnet NL
8. Small ﬁle, sequential write Ns · Lnet Ns · Lnet 1
9. Large ﬁle, sequential write NL · Lnet NL · Lnet 1
10. Large ﬁle, sequential overwrite NL · Lnet 2 · NL · Lnet 2
11. Large ﬁle, single write Lnet 2 · NL · Lnet 2 · NL
Figure 50.4: Comparison: AFS vs. NFS
50.7 Scale And Performance Of AFSv2
With the new protocol in place, AFSv2 was measured and found to
be much more scalable than the original version. Indeed, each se rver
could support about 50 clients (instead of just 20). A further ben eﬁt was
that client-side performance often came quite close to local per formance,
because in the common case, all ﬁle accesses were local; ﬁle read s usually
went to the local disk cache (and potentially , local memory). Only when a
client created a new ﬁle or wrote to an existing one was there need to send
a Store message to the server and thus update the ﬁle with new cont ents.
Let us also gain some perspective on AFS performance by compar-
ing common ﬁle-system access scenarios with NFS. Figure 50.4 (pa ge 9)
shows the results of our qualitative comparison.
In the ﬁgure, we examine typical read and write patterns anal ytically ,
for ﬁles of different sizes. Small ﬁles have Ns blocks in them; medium
ﬁles have Nm blocks; large ﬁles have NL blocks. We assume that small
and medium ﬁles ﬁt into the memory of a client; large ﬁles ﬁt on a loc al
disk but not in client memory .
We also assume, for the sake of analysis, that an access across th e net-
work to the remote server for a ﬁle block takes Lnet time units. Access
to local memory takes Lmem, and access to local disk takes Ldisk. The
general assumption is that Lnet > L disk > L mem.
Finally , we assume that the ﬁrst access to a ﬁle does not hit in an y
caches. Subsequent ﬁle accesses (i.e., “re-reads”) we assum e will hit in
caches, if the relevant cache has enough capacity to hold the ﬁl e.
The columns of the ﬁgure show the time a particular operation (e.g. , a
small ﬁle sequential read) roughly takes on either NFS or AFS. The right-
most column displays the ratio of AFS to NFS.
We make the following observations. First, in many cases, the per -
formance of each system is roughly equivalent. For example, when ﬁrst
reading a ﬁle (e.g., Workloads 1, 3, 5), the time to fetch the ﬁle from the re-
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

10 T HE ANDREW FILE SYSTEM (AFS)
mote server dominates, and is similar on both systems. You might th ink
AFS would be slower in this case, as it has to write the ﬁle to local disk;
however, those writes are buffered by the local (client-side) ﬁ le system
cache and thus said costs are likely hidden. Similarly , you migh t think
that AFS reads from the local cached copy would be slower, again be-
cause AFS stores the cached copy on disk. However, AFS again beneﬁ ts
here from local ﬁle system caching; reads on AFS would likely hit i n the
client-side memory cache, and performance would be similar to N FS.
Second, an interesting difference arises during a large-ﬁle s equential
re-read (Workload 6). Because AFS has a large local disk cache, i t will
access the ﬁle from there when the ﬁle is accessed again. NFS, in contrast,
only can cache blocks in client memory; as a result, if a large ﬁle (i.e., a ﬁle
bigger than local memory) is re-read, the NFS client will have t o re-fetch
the entire ﬁle from the remote server. Thus, AFS is faster than N FS in this
case by a factor of Lnet
Ldisk
, assuming that remote access is indeed slower
than local disk. We also note that NFS in this case increases ser ver load,
which has an impact on scale as well.
Third, we note that sequential writes (of new ﬁles) should perfor m
similarly on both systems (Workloads 8, 9). AFS, in this case, will write
the ﬁle to the local cached copy; when the ﬁle is closed, the AFS cl ient
will force the writes to the server, as per the protocol. NFS will b uffer
writes in client memory , perhaps forcing some blocks to the serve r due
to client-side memory pressure, but deﬁnitely writing them t o the server
when the ﬁle is closed, to preserve NFS ﬂush-on-close consistenc y . You
might think AFS would be slower here, because it writes all data to local
disk. However, realize that it is writing to a local ﬁle system; those writes
are ﬁrst committed to the page cache, and only later (in the back ground)
to disk, and thus AFS reaps the beneﬁts of the client-side OS me mory
caching infrastructure to improve performance.
Fourth, we note that AFS performs worse on a sequential ﬁle over-
write (Workload 10). Thus far, we have assumed that the workloads that
write are also creating a new ﬁle; in this case, the ﬁle exists , and is then
over-written. Overwrite can be a particularly bad case for AFS, because
the client ﬁrst fetches the old ﬁle in its entirety , only to subsequently over-
write it. NFS, in contrast, will simply overwrite blocks and thus avoid the
initial (useless) read 2.
Finally , workloads that access a small subset of data within lar ge ﬁles
perform much better on NFS than AFS (Workloads 7, 11). In these cas es,
the AFS protocol fetches the entire ﬁle when the ﬁle is opened; unf ortu-
nately , only a small read or write is performed. Even worse, if the ﬁle is
modiﬁed, the entire ﬁle is written back to the server, doubling the per-
2We assume here that NFS writes are block-sized and block-aligned; if t hey were not, the
NFS client would also have to read the block ﬁrst. We also assume the ﬁ le was not opened
with the O TRUNC ﬂag; if it had been, the initial open in AFS would not fetch the soon to be
truncated ﬁle’s contents.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

THE ANDREW FILE SYSTEM (AFS) 11
ASIDE : T HE IMPORTANCE OF WORKLOAD
One challenge of evaluating any system is the choice of workload. Be-
cause computer systems are used in so many different ways, the re are a
large variety of workloads to choose from. How should the storage sys-
tem designer decide which workloads are important, in order to ma ke
reasonable design decisions?
The designers of AFS, given their experience in measuring how ﬁl e sys-
tems were used, made certain workload assumptions; in particul ar, they
assumed that most ﬁles were not frequently shared, and accessed sequen-
tially in their entirety . Given those assumptions, the AFS des ign makes
perfect sense.
However, these assumptions are not always correct. For example, i mag-
ine an application that appends information, periodically , to a log. These
little log writes, which add small amounts of data to an existing large ﬁle,
are quite problematic for AFS. Many other difﬁcult workloads exist as
well, e.g., random updates in a transaction database.
One place to get some information about what types of workloads are
common are through various research studies that have been perfor med.
See any of these studies for good examples of workload analysis [B+91,
H+11, R+00, V99], including the AFS retrospective [H+88].
formance impact. NFS, as a block-based protocol, performs I/O that i s
proportional to the size of the read or write.
Overall, we see that NFS and AFS make different assumptions an d not
surprisingly realize different performance outcomes as a resu lt. Whether
these differences matter is, as always, a question of workload.
50.8 AFS: Other Improvements
Like we saw with the introduction of Berkeley FFS (which added sy m-
bolic links and a number of other features), the designers of AFS t ook the
opportunity when building their system to add a number of featur es that
made the system easier to use and manage. For example, AFS provi des a
true global namespace to clients, thus ensuring that all ﬁles were named
the same way on all client machines. NFS, in contrast, allows each client
to mount NFS servers in any way that they please, and thus only by con-
vention (and great administrative effort) would ﬁles be named s imilarly
across clients.
AFS also takes security seriously , and incorporates mechanisms to au-
thenticate users and ensure that a set of ﬁles could be kept priv ate if a
user so desired. NFS, in contrast, had quite primitive support f or security
for many years.
AFS also includes facilities for ﬂexible user-managed acces s control.
Thus, when using AFS, a user has a great deal of control over who exac tly
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

12 T HE ANDREW FILE SYSTEM (AFS)
can access which ﬁles. NFS, like most U NIX ﬁle systems, has much less
support for this type of sharing.
Finally , as mentioned before, AFS adds tools to enable simpler ma n-
agement of servers for the administrators of the system. In thinking about
system management, AFS was light years ahead of the ﬁeld.
50.9 Summary
AFS shows us how distributed ﬁle systems can be built quite diff er-
ently than what we saw with NFS. The protocol design of AFS is partic -
ularly important; by minimizing server interactions (through whole-ﬁle
caching and callbacks), each server can support many clients and thus
reduce the number of servers needed to manage a particular sit e. Many
other features, including the single namespace, security , and access-control
lists, make AFS quite nice to use. The consistency model provided by AFS
is simple to understand and reason about, and does not lead to the oc ca-
sional weird behavior as one sometimes observes in NFS.
Perhaps unfortunately , AFS is likely on the decline. Because N FS be-
came an open standard, many different vendors supported it, and , along
with CIFS (the Windows-based distributed ﬁle system protocol), NFS
dominates the marketplace. Although one still sees AFS install ations
from time to time (such as in various educational institutions, i ncluding
Wisconsin), the only lasting inﬂuence will likely be from the id eas of AFS
rather than the actual system itself. Indeed, NFSv4 now adds se rver state
(e.g., an “open” protocol message), and thus bears an increasing similar-
ity to the basic AFS protocol.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

THE ANDREW FILE SYSTEM (AFS) 13
References
[B+91] “Measurements of a Distributed File System” by Mary Baker , John Hartman, Martin
Kupfer, Ken Shirriff, John Ousterhout. SOSP ’91, Paciﬁc Grove, Californi a, October 1991. An
early paper measuring how people use distributed ﬁle systems. Matches m uch of the intuition found in
AFS.
[H+11] “A File is Not a File: Understanding the I/O Behavior of Apple Desktop Applications”
by Tyler Harter, Chris Dragga, Michael Vaughn, Andrea C. Arpaci-Dusseau, Remzi H. Arpaci-
Dusseau. SOSP ’11, New York, New York, October 2011. Our own paper studying the behavior of
Apple Desktop workloads; turns out they are a bit different than many of the serv er-based workloads the
systems research community usually focuses upon. Also a good recent re ference which points to a lot of
related work.
[H+88] “Scale and Performance in a Distributed File System” by John H. H oward, Michael
L. Kazar, Sherri G. Menees, David A. Nichols, M. Satyanarayanan, Rober t N. Sidebotham,
Michael J. West. ACM Transactions on Computing Systems (ACM TOCS), V olum e 6:1, Febru-
ary 1988. The long journal version of the famous AFS system, still in use in a number of places
throughout the world, and also probably the earliest clear thinking on how to bui ld distributed ﬁle
systems. A wonderful combination of the science of measurement and princ ipled engineering.
[R+00] “A Comparison of File System Workloads” by Drew Rosell i, Jacob R. Lorch, Thomas E.
Anderson. USENIX ’00, San Diego, California, June 2000. A more recent set of traces as compared
to the Baker paper [B+91], with some interesting twists.
[S+85] “The ITC Distributed File System: Principles and Design” by M. Sa tyanarayanan, J.H.
Howard, D.A. Nichols, R.N. Sidebotham, A. Spector, M.J. West. SOSP ’ 85, Orcas Island, Wash-
ington, December 1985. The older paper about a distributed ﬁle system. Much of the basic design of
AFS is in place in this older system, but not the improvements for scale. T he name change to “Andrew”
is an homage to two people both named Andrew, Andrew Carnegie and Andrew Me llon. These two
rich dudes started the Carnegie Institute of T echnology and the Mellon Institute of Industrial Research,
respectively, which eventually merged to become what is now known as Carn egie Mellon University.
[V99] “File system usage in Windows NT 4.0” by Werner V ogels. SOSP ’99, Kiawah Island
Resort, South Carolina, December 1999. A cool study of Windows workloads, which are inherently
different than many of the UNIX -based studies that had previously been done.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

14 T HE ANDREW FILE SYSTEM (AFS)
Homework (Simulation)
This section introduces afs.py, a simple AFS simulator you can use
to shore up your knowledge of how the Andrew File System works. Read
the README ﬁle for more details.
Questions
1. Run a few simple cases to make sure you can predict what value s
will be read by clients. Vary the random seed ﬂag ( -s) and see
if you can trace through and predict both intermediate values as
well as the ﬁnal values stored in the ﬁles. Also vary the number of
ﬁles ( -f), the number of clients ( -C), and the read ratio ( -r, from
between 0 to 1) to make it a bit more challenging. You might also
want to generate slightly longer traces to make for more interes ting
interactions, e.g., ( -n 2 or higher).
2. Now do the same thing and see if you can predict each callback t hat
the AFS server initiates. Try different random seeds, and mak e sure
to use a high level of detailed feedback (e.g., -d 3 ) to see when call-
backs occur when you have the program compute the answers for
you (with -c). Can you guess exactly when each callback occurs?
What is the precise condition for one to take place?
3. Similar to above, run with some different random seeds and see i f
you can predict the exact cache state at each step. Cache state can
be observed by running with -c and -d 7 .
4. Now let’s construct some speciﬁc workloads. Run the simulation
with -A oa1:w1:c1,oa1:r1:c1 ﬂag. What are different possi-
ble values observed by client 1 when it reads the ﬁle a, when run-
ning with the random scheduler? (try different random seeds to
see different outcomes)? Of all the possible schedule interlea vings
of the two clients’ operations, how many of them lead to client 1
reading the value 1, and how many reading the value 0?
5. Now let’s construct some speciﬁc schedules. When running with
the -A oa1:w1:c1,oa1:r1:c1 ﬂag, also run with the following
schedules: -S 01 , -S 100011 , -S 011100 , and others of which
you can think. What value will client 1 read?
6. Now run with this workload: -A oa1:w1:c1,oa1:w1:c1 , and
vary the schedules as above. What happens when you run with -S
011100? What about when you run with -S 010011 ? What is
important in determining the ﬁnal value of the ﬁle?
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
