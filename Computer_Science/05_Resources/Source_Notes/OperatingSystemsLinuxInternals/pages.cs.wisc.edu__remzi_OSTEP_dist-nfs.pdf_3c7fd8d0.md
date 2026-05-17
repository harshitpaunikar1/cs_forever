Title: dist-nfs.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/dist-nfs.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:17+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

49
Sun’s Network File System (NFS)
One of the ﬁrst uses of distributed client/server computing was in the
realm of distributed ﬁle systems. In such an environment, ther e are a
number of client machines and one server (or a few); the server st ores the
data on its disks, and clients request data through well-formed protocol
messages. Figure 49.1 depicts the basic setup.
Client 0
Client 1
Client 2
Client 3
Server
RAID
Network
Figure 49.1: A Generic Client/Server System
As you can see from the picture, the server has the disks, and cli ents
send messages across a network to access their directories and ﬁ les on
those disks. Why do we bother with this arrangement? (i.e., why don’t
we just let clients use their local disks?) Well, primarily th is setup allows
for easy sharing of data across clients. Thus, if you access a ﬁle on one
machine (Client 0) and then later use another (Client 2), you wi ll have the
same view of the ﬁle system. Your data is naturally shared across these
different machines. A secondary beneﬁt is centralized administration ;
for example, backing up ﬁles can be done from the few server machi nes
instead of from the multitude of clients. Another advantage could be
security; having all servers in a locked machine room prevents certain
types of problems from arising.
1

2 S UN’ S NETWORK FILE SYSTEM (NFS)
CRUX : H OW TO BUILD A D ISTRIBUTED FILE SYSTEM
How do you build a distributed ﬁle system? What are the key aspec ts
to think about? What is easy to get wrong? What can we learn from
existing systems?
49.1 A Basic Distributed File System
We now will study the architecture of a simpliﬁed distributed ﬁ le sys-
tem. A simple client/server distributed ﬁle system has more c omponents
than the ﬁle systems we have studied so far. On the client side , there are
client applications which access ﬁles and directories through the client-
side ﬁle system . A client application issues system calls to the client-side
ﬁle system (such as open(), read(), write(), close(), mkdir(),
etc.) in order to access ﬁles which are stored on the server. Thus , to client
applications, the ﬁle system does not appear to be any different than a lo-
cal (disk-based) ﬁle system, except perhaps for performance; in this way ,
distributed ﬁle systems provide transparent access to ﬁles, an obvious
goal; after all, who would want to use a ﬁle system that required a differ-
ent set of APIs or otherwise was a pain to use?
The role of the client-side ﬁle system is to execute the actions n eeded
to service those system calls. For example, if the client issue s a read()
request, the client-side ﬁle system may send a message to the server-side
ﬁle system (or, as it is commonly called, the ﬁle server ) to read a partic-
ular block; the ﬁle server will then read the block from disk (or it s own
in-memory cache), and send a message back to the client with th e re-
quested data. The client-side ﬁle system will then copy the da ta into the
user buffer supplied to the read() system call and thus the request will
complete. Note that a subsequent read() of the same block on the client
may be cached in client memory or on the client’s disk even; in the best
such case, no network trafﬁc need be generated.
Client Application
Client-side File System
Networking Layer
File Server
Networking Layer
Disks
Figure 49.2: Distributed File System Architecture
From this simple overview, you should get a sense that there are tw o
important pieces of software in a client/server distributed ﬁl e system: the
client-side ﬁle system and the ﬁle server. Together their beh avior deter-
mines the behavior of the distributed ﬁle system. Now it’s time to study
one particular system: Sun’s Network File System (NFS).
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

SUN’ S NETWORK FILE SYSTEM (NFS) 3
ASIDE : W HY SERVERS CRASH
Before getting into the details of the NFSv2 protocol, you might be
wondering: why do servers crash? Well, as you might guess, ther e are
plenty of reasons. Servers may simply suffer from a power outage (tem-
porarily); only when power is restored can the machines be restar ted.
Servers are often comprised of hundreds of thousands or even millions
of lines of code; thus, they have bugs (even good software has a few
bugs per hundred or thousand lines of code), and thus they eventua lly
will trigger a bug that will cause them to crash. They also hav e memory
leaks; even a small memory leak will cause a system to run out of me m-
ory and crash. And, ﬁnally , in distributed systems, there is a network
between the client and the server; if the network acts strange ly (for ex-
ample, if it becomes partitioned and clients and servers are working but
cannot communicate), it may appear as if a remote machine has cra shed,
but in reality it is just not currently reachable through the ne twork.
49.2 On To NFS
One of the earliest and quite successful distributed systems was devel-
oped by Sun Microsystems, and is known as the Sun Network File Sys-
tem (or NFS) [S86]. In deﬁning NFS, Sun took an unusual approach: in-
stead of building a proprietary and closed system, Sun instead de veloped
an open protocol which simply speciﬁed the exact message formats that
clients and servers would use to communicate. Different groups could
develop their own NFS servers and thus compete in an NFS marketpl ace
while preserving interoperability . It worked: today there are many com-
panies that sell NFS servers (including Oracle/Sun, NetApp [ HLM94],
EMC, IBM, and others), and the widespread success of NFS is like ly at-
tributed to this “open market” approach.
49.3 Focus: Simple And Fast Server Crash Recovery
In this chapter, we will discuss the classic NFS protocol (versi on 2,
a.k.a. NFSv2), which was the standard for many years; small cha nges
were made in moving to NFSv3, and larger-scale protocol changes we re
made in moving to NFSv4. However, NFSv2 is both wonderful and frus-
trating and thus serves as our focus.
In NFSv2, the main goal in the design of the protocol was simple and
fast server crash recovery . In a multiple-client, single-server environment,
this goal makes a great deal of sense; any minute that the server is down
(or unavailable) makes all the client machines (and their users) unhappy
and unproductive. Thus, as the server goes, so goes the entire sy stem.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

4 S UN’ S NETWORK FILE SYSTEM (NFS)
49.4 Key To Fast Crash Recovery: Statelessness
This simple goal is realized in NFSv2 by designing what we refer to
as a stateless protocol. The server, by design, does not keep track of any-
thing about what is happening at each client. For example, the s erver
does not know which clients are caching which blocks, or which ﬁles are
currently open at each client, or the current ﬁle pointer position for a ﬁle,
etc. Simply put, the server does not track anything about what cli ents are
doing; rather, the protocol is designed to deliver in each protocol r equest
all the information that is needed in order to complete the request. If it
doesn’t now, this stateless approach will make more sense as we dis cuss
the protocol in more detail below.
For an example of a stateful (not stateless) protocol, consider the open()
system call. Given a pathname, open() returns a ﬁle descriptor (an inte-
ger). This descriptor is used on subsequent read() or write() requests
to access various ﬁle blocks, as in this application code (note tha t proper
error checking of the system calls is omitted for space reasons):
char buffer[MAX];
int fd = open("foo", O_RDONLY); // get descriptor "fd"
read(fd, buffer, MAX); // read MAX from foo via "fd"
read(fd, buffer, MAX); // read MAX again
...
read(fd, buffer, MAX); // read MAX again
close(fd); // close file
Figure 49.3: Client Code: Reading From A File
Now imagine that the client-side ﬁle system opens the ﬁle by sen ding
a protocol message to the server saying “open the ﬁle ’foo’ and give me
back a descriptor”. The ﬁle server then opens the ﬁle locally on it s side
and sends the descriptor back to the client. On subsequent rea ds, the
client application uses that descriptor to call the read() system call; the
client-side ﬁle system then passes the descriptor in a messag e to the ﬁle
server, saying “read some bytes from the ﬁle that is referred to by the
descriptor I am passing you here”.
In this example, the ﬁle descriptor is a piece of shared state between
the client and the server (Ousterhout calls this distributed state [O91]).
Shared state, as we hinted above, complicates crash recovery . Im agine
the server crashes after the ﬁrst read completes, but before th e client
has issued the second one. After the server is up and running aga in,
the client then issues the second read. Unfortunately , the ser ver has no
idea to which ﬁle fd is referring; that information was ephemeral (i.e.,
in memory) and thus lost when the server crashed. To handle this situa-
tion, the client and server would have to engage in some kind of recovery
protocol, where the client would make sure to keep enough information
around in its memory to be able to tell the server what it needs to know
(in this case, that ﬁle descriptor fd refers to ﬁle foo).
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

SUN’ S NETWORK FILE SYSTEM (NFS) 5
It gets even worse when you consider the fact that a stateful serv er has
to deal with client crashes. Imagine, for example, a client th at opens a ﬁle
and then crashes. The open() uses up a ﬁle descriptor on the server; how
can the server know it is OK to close a given ﬁle? In normal operation , a
client would eventually call close() and thus inform the server that the
ﬁle should be closed. However, when a client crashes, the server never
receives a close(), and thus has to notice the client has crashed in order
to close the ﬁle.
For these reasons, the designers of NFS decided to pursue a state less
approach: each client operation contains all the information need ed to
complete the request. No fancy crash recovery is needed; the se rver just
starts running again, and a client, at worst, might have to ret ry a request.
49.5 The NFSv2 Protocol
We thus arrive at the NFSv2 protocol deﬁnition. Our problem state-
ment is simple:
THE CRUX : H OW TO DEFINE A S TATELESS FILE PROTOCOL
How can we deﬁne the network protocol to enable stateless operation?
Clearly , stateful calls like open() can’t be a part of the discussion (as it
would require the server to track open ﬁles); however, the clien t appli-
cation will want to call open(), read(), write(), close() and other
standard API calls to access ﬁles and directories. Thus, as a r eﬁned ques-
tion, how do we deﬁne the protocol to both be stateless and support the
POSIX ﬁle system API?
One key to understanding the design of the NFS protocol is under-
standing the ﬁle handle . File handles are used to uniquely describe the
ﬁle or directory a particular operation is going to operate upon; thu s,
many of the protocol requests include a ﬁle handle.
You can think of a ﬁle handle as having three important components: a
volume identiﬁer , an inode number, and a generation number; together, these
three items comprise a unique identiﬁer for a ﬁle or directory tha t a client
wishes to access. The volume identiﬁer informs the server whic h ﬁle sys-
tem the request refers to (an NFS server can export more than one ﬁ le
system); the inode number tells the server which ﬁle within th at partition
the request is accessing. Finally , the generation number is n eeded when
reusing an inode number; by incrementing it whenever an inode n um-
ber is reused, the server ensures that a client with an old ﬁle h andle can’t
accidentally access the newly-allocated ﬁle.
Here is a summary of some of the important pieces of the protocol; the
full protocol is available elsewhere (see Callaghan’s book for an ex cellent
and detailed overview of NFS [C00]).
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

6 S UN’ S NETWORK FILE SYSTEM (NFS)
NFSPROC_GETATTR ﬁle handle
returns: attributes
NFSPROC_SETATTR ﬁle handle, attributes
returns: attributes
NFSPROC_LOOKUP directory ﬁle handle, name of ﬁle/dir to look up
returns: ﬁle handle, attributes
NFSPROC_READ ﬁle handle, offset, count
data, attributes
NFSPROC_WRITE ﬁle handle, offset, count, data
attributes
NFSPROC_CREATE directory ﬁle handle, name of ﬁle, attributes
ﬁle handle, attributes
NFSPROC_REMOVE directory ﬁle handle, name of ﬁle to be removed
–
NFSPROC_MKDIR directory ﬁle handle, name of directory , attributes
ﬁle handle, attributes
NFSPROC_RMDIR directory ﬁle handle, name of directory to be removed
–
NFSPROC_READDIR directory handle, count of bytes to read, cookie
returns: directory entries, cookie (to get more entries)
Figure 49.4: The NFS Protocol: Examples
We brieﬂy highlight the important components of the protocol. First ,
the LOOKUP protocol message is used to obtain a ﬁle handle, which i s
then subsequently used to access ﬁle data. The client passes a directory
ﬁle handle and name of a ﬁle to look up, and the handle to that ﬁle (or
directory) plus its attributes are passed back to the client f rom the server.
For example, assume the client already has a directory ﬁle hand le for
the root directory of a ﬁle system ( /) (indeed, this would be obtained
through the NFS mount protocol , which is how clients and servers ﬁrst
are connected together; we do not discuss the mount protocol here for
sake of brevity). If an application running on the client opens th e ﬁle
/foo.txt, the client-side ﬁle system sends a lookup request to the serve r,
passing it the root ﬁle handle and the name foo.txt; if successful, the
ﬁle handle (and attributes) for foo.txt will be returned.
In case you are wondering, attributes are just the metadata tha t the ﬁle
system tracks about each ﬁle, including ﬁelds such as ﬁle crea tion time,
last modiﬁcation time, size, ownership and permissions informat ion, and
so forth, i.e., the same type of information that you would get back i f you
called stat() on a ﬁle.
Once a ﬁle handle is available, the client can issue READ and W RITE
protocol messages on a ﬁle to read or write the ﬁle, respectively . T he
READ protocol message requires the protocol to pass along the ﬁle han dle
of the ﬁle along with the offset within the ﬁle and number of bytes t o read.
The server then will be able to issue the read (after all, the h andle tells the
server which volume and which inode to read from, and the offset an d
count tells it which bytes of the ﬁle to read) and return the data (and up-
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

SUN’ S NETWORK FILE SYSTEM (NFS) 7
to-date attributes) to the client (or an error if there was a fail ure). WRITE
is handled similarly , except the data is passed from the client to the server,
and just a success code (and up-to-date attributes) is returne d.
One last interesting protocol message is the GETATTR request; given a
ﬁle handle, it simply fetches the attributes for that ﬁle, inc luding the last
modiﬁed time of the ﬁle. We will see why this protocol request is imp or-
tant in NFSv2 below when we discuss caching (can you guess why?).
49.6 From Protocol To Distributed File System
Hopefully you are now getting some sense of how this protocol is
turned into a ﬁle system across the client-side ﬁle system and the ﬁle
server. The client-side ﬁle system tracks open ﬁles, and gene rally trans-
lates application requests into the relevant set of protocol mess ages. The
server simply responds to protocol messages, each of which contain s all
of the information needed to complete the request.
For example, let us consider a simple application which reads a ﬁ le.
In the diagram (Figure 49.5), we show what system calls the app lication
makes, and what the client-side ﬁle system and ﬁle server do i n respond-
ing to such calls.
A few comments about the ﬁgure. First, notice how the client track s all
relevant state for the ﬁle access, including the mapping of the integer ﬁle
descriptor to an NFS ﬁle handle as well as the current ﬁle pointe r. This
enables the client to turn each read request (which you may hav e noticed
do not specify the offset to read from explicitly) into a properly-form atted
read protocol message which tells the server exactly which byte s from
the ﬁle to read. Upon a successful read, the client updates the current
ﬁle position; subsequent reads are issued with the same ﬁle han dle but a
different offset.
Second, you may notice where server interactions occur. When the ﬁl e
is opened for the ﬁrst time, the client-side ﬁle system sends a L OOKUP
request message. Indeed, if a long pathname must be traversed (e.g.,
/home/remzi/foo.txt), the client would send three LOOKUPs: one
to look up home in the directory /, one to look up remzi in home, and
ﬁnally one to look up foo.txt in remzi.
Third, you may notice how each server request has all the informat ion
needed to complete the request in its entirety . This design poi nt is critical
to be able to gracefully recover from server failure, as we will now discuss
in more detail; it ensures that the server does not need state to b e able to
respond to the request.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

8 S UN’ S NETWORK FILE SYSTEM (NFS)
Client Server
fd = open(”/foo”, ...);
Send LOOKUP (rootdir FH, ”foo”)
Receive LOOKUP request
look for ”foo” in root dir
return foo’s FH + attributes
Receive LOOKUP reply
allocate ﬁle desc in open ﬁle table
store foo’s FH in table
store current ﬁle position (0)
return ﬁle descriptor to application
read(fd, buffer, MAX);
Index into open ﬁle table with fd
get NFS ﬁle handle (FH)
use current ﬁle position as offset
Send READ (FH, offset=0, count=MAX)
Receive READ request
use FH to get volume/inode num
read inode from disk (or cache)
compute block location (using offset)
read data from disk (or cache)
return data to client
Receive READ reply
update ﬁle position (+bytes read)
set current ﬁle position = MAX
return data/error code to app
read(fd, buffer, MAX);
Same except offset=MAX and set current ﬁle position = 2*MAX
read(fd, buffer, MAX);
Same except offset=2*MAX and set current ﬁle position = 3*MAX
close(fd);
Just need to clean up local structures
Free descriptor ”fd” in open ﬁle table
(No need to talk to server)
Figure 49.5: Reading A File: Client-side And File Server Actions
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

SUN’ S NETWORK FILE SYSTEM (NFS) 9
TIP : I DEMPOTENCY IS POWERFUL
Idempotency is a useful property when building reliable systems. When
an operation can be issued more than once, it is much easier to hand le
failure of the operation; you can just retry it. If an operation is not idem-
potent, life becomes more difﬁcult.
49.7 Handling Server Failure With Idempotent Operations
When a client sends a message to the server, it sometimes does not re-
ceive a reply . There are many possible reasons for this failure t o respond.
In some cases, the message may be dropped by the network; networks do
lose messages, and thus either the request or the reply could be l ost and
thus the client would never receive a response.
It is also possible that the server has crashed, and thus is not c urrently
responding to messages. After a bit, the server will be rebooted and start
running again, but in the meanwhile all requests have been los t. In all of
these cases, clients are left with a question: what should they do when
the server does not reply in a timely manner?
In NFSv2, a client handles all of these failures in a single, uni form, and
elegant way: it simply retries the request. Speciﬁcally , after sending the
request, the client sets a timer to go off after a speciﬁed time period. If a
reply is received before the timer goes off, the timer is cancele d and all is
well. If, however, the timer goes off before any reply is received, the client
assumes the request has not been processed and resends it. If th e server
replies, all is well and the client has neatly handled the prob lem.
The ability of the client to simply retry the request (regardl ess of what
caused the failure) is due to an important property of most NFS req uests:
they are idempotent. An operation is called idempotent when the effect
of performing the operation multiple times is equivalent to the e ffect of
performing the operation a single time. For example, if you store a v alue
to a memory location three times, it is the same as doing so once; thu s
“store value to memory” is an idempotent operation. If, however, you in-
crement a counter three times, it results in a different amount than doing
so just once; thus, “increment counter” is not idempotent. More ge ner-
ally , any operation that just reads data is obviously idempotent; an oper-
ation that updates data must be more carefully considered to det ermine
if it has this property .
The heart of the design of crash recovery in NFS is the idempotency
of most common operations. LOOKUP and READ requests are trivially
idempotent, as they only read information from the ﬁle server and d o not
update it. More interestingly , WRITE requests are also idemp otent. If,
for example, a WRITE fails, the client can simply retry it. The WRITE
message contains the data, the count, and (importantly) the exa ct offset
to write the data to. Thus, it can be repeated with the knowledge that the
outcome of multiple writes is the same as the outcome of a single one.
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

10 S UN’ S NETWORK FILE SYSTEM (NFS)
Case 1: Request Lost
Client
[send request]
Server
(no mesg)
Case 2: Server Down
Client
[send request]
Server
(down)
Case 3: Reply lost on way back from Server
Client
[send request]
Server
[recv request]
[handle request]
[send reply]
Figure 49.6: The Three Types Of Loss
In this way , the client can handle all timeouts in a uniﬁed way . If a
WRITE request was simply lost (Case 1 above), the client will re try it, the
server will perform the write, and all will be well. The same wi ll happen
if the server happened to be down while the request was sent, bu t back
up and running when the second request is sent, and again all wor ks
as desired (Case 2). Finally , the server may in fact receive t he WRITE
request, issue the write to its disk, and send a reply . This re ply may get
lost (Case 3), again causing the client to re-send the request . When the
server receives the request again, it will simply do the exac t same thing:
write the data to disk and reply that it has done so. If the client this time
receives the reply , all is again well, and thus the client has handled both
message loss and server failure in a uniform manner. Neat!
A small aside: some operations are hard to make idempotent. For
example, when you try to make a directory that already exists, y ou are
informed that the mkdir request has failed. Thus, in NFS, if the ﬁle server
receives a MKDIR protocol message and executes it successfully but the
reply is lost, the client may repeat it and encounter that failu re when in
fact the operation at ﬁrst succeeded and then only failed on the re try .
Thus, life is not perfect.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

SUN’ S NETWORK FILE SYSTEM (NFS) 11
TIP : P ERFECT IS THE ENEMY OF THE GOOD (V OLTAIRE ’ S LAW)
Even when you design a beautiful system, sometimes all the corne r cases
don’t work out exactly as you might like. Take the mkdir example abov e;
one could redesign mkdir to have different semantics, thus mak ing it
idempotent (think about how you might do so); however, why bother?
The NFS design philosophy covers most of the important cases, and ove r-
all makes the system design clean and simple with regards to f ailure.
Thus, accepting that life isn’t perfect and still building th e system is a sign
of good engineering. Apparently , this wisdom is attributed to V ol taire,
for saying “... a wise Italian says that the best is the enemy of t he good”
[V72], and thus we call it V oltaire’s Law.
49.8 Improving Performance: Client-side Caching
Distributed ﬁle systems are good for a number of reasons, but sendi ng
all read and write requests across the network can lead to a big p erfor-
mance problem: the network generally isn’t that fast, especial ly as com-
pared to local memory or disk. Thus, another problem: how can we im-
prove the performance of a distributed ﬁle system?
The answer, as you might guess from reading the big bold words in
the sub-heading above, is client-side caching. The NFS client-side ﬁle
system caches ﬁle data (and metadata) that it has read from the server in
client memory . Thus, while the ﬁrst access is expensive (i.e. , it requires
network communication), subsequent accesses are serviced qui te quickly
out of client memory .
The cache also serves as a temporary buffer for writes. When a cl ient
application ﬁrst writes to a ﬁle, the client buffers the data i n client mem-
ory (in the same cache as the data it read from the ﬁle server) bef ore writ-
ing the data out to the server. Such write buffering is useful because it de-
couples application write() latency from actual write performance, i.e.,
the application’s call to write() succeeds immediately (and just puts
the data in the client-side ﬁle system’s cache); only later does the data get
written out to the ﬁle server.
Thus, NFS clients cache data and performance is usually great and
we are done, right? Unfortunately , not quite. Adding caching in to any
sort of system with multiple client caches introduces a big and i nteresting
challenge which we will refer to as the cache consistency problem .
49.9 The Cache Consistency Problem
The cache consistency problem is best illustrated with three clients and
a single server. Imagine client C1 reads a ﬁle F, and keeps a cop y of the
ﬁle in its local cache. Now imagine a different client, C2, overw rites the
ﬁle F, thus changing its contents; let’s call the new version of th e ﬁle F
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

12 S UN’ S NETWORK FILE SYSTEM (NFS)
C1
cache: F[v1]
C2
cache: F[v2]
C3
cache: empty
Server S
disk: F[v1] at first
F[v2] eventually
Figure 49.7: The Cache Consistency Problem
(version 2), or F[v2] and the old version F[v1] so we can keep the tw o
distinct (but of course the ﬁle has the same name, just differen t contents).
Finally , there is a third client, C3, which has not yet accesse d the ﬁle F.
You can probably see the problem that is upcoming (Figure 49.7). I n
fact, there are two subproblems. The ﬁrst subproblem is that th e client C2
may buffer its writes in its cache for a time before propagating them to the
server; in this case, while F[v2] sits in C2’s memory , any acces s of F from
another client (say C3) will fetch the old version of the ﬁle (F[v1 ]). Thus,
by buffering writes at the client, other clients may get stale versions of the
ﬁle, which may be undesirable; indeed, imagine the case wher e you log
into machine C2, update F, and then log into C3 and try to read th e ﬁle,
only to get the old copy! Certainly this could be frustrating. Thu s, let us
call this aspect of the cache consistency problem update visibility; when
do updates from one client become visible at other clients?
The second subproblem of cache consistency is a stale cache ; in this
case, C2 has ﬁnally ﬂushed its writes to the ﬁle server, and th us the server
has the latest version (F[v2]). However, C1 still has F[v1] in i ts cache; if a
program running on C1 reads ﬁle F, it will get a stale version (F[v 1]) and
not the most recent copy (F[v2]), which is (often) undesirable.
NFSv2 implementations solve these cache consistency problems in two
ways. First, to address update visibility , clients impleme nt what is some-
times called ﬂush-on-close (a.k.a., close-to-open) consistency semantics;
speciﬁcally , when a ﬁle is written to and subsequently closed by a client
application, the client ﬂushes all updates (i.e., dirty page s in the cache)
to the server. With ﬂush-on-close consistency , NFS ensures tha t a subse-
quent open from another node will see the latest ﬁle version.
Second, to address the stale-cache problem, NFSv2 clients ﬁrst c heck
to see whether a ﬁle has changed before using its cached content s. Specif-
ically , before using a cached block, the client-side ﬁle syste m will issue a
GETATTR request to the server to fetch the ﬁle’s attributes. T he attributes,
importantly , include information as to when the ﬁle was last modi ﬁed on
the server; if the time-of-modiﬁcation is more recent than the ti me that the
ﬁle was fetched into the client cache, the client invalidates the ﬁle, thus
removing it from the client cache and ensuring that subsequent reads will
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

SUN’ S NETWORK FILE SYSTEM (NFS) 13
go to the server and retrieve the latest version of the ﬁle. If, on the other
hand, the client sees that it has the latest version of the ﬁle, i t will go
ahead and use the cached contents, thus increasing performanc e.
When the original team at Sun implemented this solution to the sta le-
cache problem, they realized a new problem; suddenly , the NFS s erver
was ﬂooded with GETATTR requests. A good engineering principle t o
follow is to design for the common case, and to make it work well; here,
although the common case was that a ﬁle was accessed only from a sin-
gle client (perhaps repeatedly), the client always had to se nd GETATTR
requests to the server to make sure no one else had changed the ﬁ le. A
client thus bombards the server, constantly asking “has anyone changed
this ﬁle?”, when most of the time no one had.
To remedy this situation (somewhat), an attribute cache was added
to each client. A client would still validate a ﬁle before acces sing it, but
most often would just look in the attribute cache to fetch the attri butes.
The attributes for a particular ﬁle were placed in the cache wh en the ﬁle
was ﬁrst accessed, and then would timeout after a certain amount of time
(say 3 seconds). Thus, during those three seconds, all ﬁle acces ses would
determine that it was OK to use the cached ﬁle and thus do so wit h no
network communication with the server.
49.10 Assessing NFS Cache Consistency
A few ﬁnal words about NFS cache consistency . The ﬂush-on-close be -
havior was added to “make sense”, but introduced a certain perf ormance
problem. Speciﬁcally , if a temporary or short-lived ﬁle was creat ed on a
client and then soon deleted, it would still be forced to the serve r. A more
ideal implementation might keep such short-lived ﬁles in memor y until
they are deleted and thus remove the server interaction entire ly , perhaps
increasing performance.
More importantly , the addition of an attribute cache into NFS mad e
it very hard to understand or reason about exactly what version of a ﬁle
one was getting. Sometimes you would get the latest version; sometim es
you would get an old version simply because your attribute cache ha dn’t
yet timed out and thus the client was happy to give you what was in
client memory . Although this was ﬁne most of the time, it would (and
still does!) occasionally lead to odd behavior.
And thus we have described the oddity that is NFS client cachin g.
It serves as an interesting example where details of an implem entation
serve to deﬁne user-observable semantics, instead of the other way around.
49.11 Implications On Server-Side Write Buffering
Our focus so far has been on client caching, and that is where most
of the interesting issues arise. However, NFS servers tend to b e well-
equipped machines with a lot of memory too, and thus they have cachi ng
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

14 S UN’ S NETWORK FILE SYSTEM (NFS)
concerns as well. When data (and metadata) is read from disk, NF S
servers will keep it in memory , and subsequent reads of said dat a (and
metadata) will not go to disk, a potential (small) boost in perform ance.
More intriguing is the case of write buffering. An NFS server ab so-
lutely may not return success on a WRITE protocol request until the write
has been forced to stable storage (e.g., to disk or some other persi stent
device). While the server can place a copy of the data in its memor y , re-
turning success to the client on a WRITE protocol request could res ult in
incorrect behavior; can you ﬁgure out why?
The answer lies in our assumptions about how clients handle serve r
failure. Imagine the following sequence of writes as issued by a client:
write(fd, a_buffer, size); // fill 1st block with a’s
write(fd, b_buffer, size); // fill 2nd block with b’s
write(fd, c_buffer, size); // fill 3rd block with c’s
These writes overwrite the three blocks of a ﬁle with a block of a’s,
then b’s, and then c’s. Thus, if the ﬁle initially looked like this :
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy
zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz
We might expect the ﬁnal result after these writes to be like t his, with the
x’s, y’s, and z’s, would be overwritten with a’s, b’s, and c’s, respect ively .
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
cccccccccccccccccccccccccccccccccccccccccccc
Now let’s assume for the sake of the example that these three clien t
writes were issued to the server as three distinct WRITE protoc ol mes-
sages. Assume the ﬁrst WRITE message is received by the serve r and
issued to the disk, and the client informed of its success. Now as sume
the second write is just buffered in memory , and the server also reports
it success to the client before forcing it to disk; unfortunately , the server
crashes before writing it to disk. The server quickly restart s and receives
the third write request, which also succeeds.
Thus, to the client, all the requests succeeded, but we are su rprised
that the ﬁle contents look like this:
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy <--- oop s
cccccccccccccccccccccccccccccccccccccccccccc
Yikes! Because the server told the client that the second write was
successful before committing it to disk, an old chunk is left in t he ﬁle,
which, depending on the application, might be catastrophic.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

SUN’ S NETWORK FILE SYSTEM (NFS) 15
ASIDE : I NNOVATION BREEDS INNOVATION
As with many pioneering technologies, bringing NFS into the worl d also
required other fundamental innovations to enable its success. Probably
the most lasting is the Virtual File System (VFS) / Virtual Node (vnode)
interface, introduced by Sun to allow different ﬁle systems to b e readily
plugged into the operating system [K86].
The VFS layer includes operations that are done to an entire ﬁle s ystem,
such as mounting and unmounting, getting ﬁle-system wide stat istics,
and forcing all dirty (not yet written) writes to disk. The vnode layer
consists of all operations one can perform on a ﬁle, such as open, close,
reads, writes, and so forth.
To build a new ﬁle system, one simply has to deﬁne these “methods ”; the
framework then handles the rest, connecting system calls to the particular
ﬁle system implementation, performing generic functions common to all
ﬁle systems (e.g., caching) in a centralized manner, and thu s providing a
way for multiple ﬁle system implementations to operate simulta neously
within the same system.
Although some of the details have changed, many modern systems ha ve
some form of a VFS/vnode layer, including Linux, BSD variants, macO S,
and even Windows (in the form of the Installable File System). Eve n if
NFS becomes less relevant to the world, some of the necessary found a-
tions beneath it will live on.
To avoid this problem, NFS servers must commit each write to stable
(persistent) storage before informing the client of success; doi ng so en-
ables the client to detect server failure during a write, and thus retry until
it ﬁnally succeeds. Doing so ensures we will never end up with ﬁ le con-
tents intermingled as in the above example.
The problem that this requirement gives rise to in NFS server i m-
plementation is that write performance, without great care, ca n be the
major performance bottleneck. Indeed, some companies (e.g., Net work
Appliance) came into existence with the simple objective of bu ilding an
NFS server that can perform writes quickly; one trick they use i s to ﬁrst
put writes in a battery-backed memory , thus enabling to quick ly reply
to WRITE requests without fear of losing the data and without the c ost
of having to write to disk right away; the second trick is to use a ﬁle sys-
tem design speciﬁcally designed to write to disk quickly whe n one ﬁnally
needs to do so [HLM94, RO91].
49.12 Summary
We have seen the introduction of the NFS distributed ﬁle system. NFS
is centered around the idea of simple and fast recovery in the fac e of
server failure, and achieves this end through careful protocol design. Idem-
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

16 S UN’ S NETWORK FILE SYSTEM (NFS)
ASIDE : K EY NFS T ERMS
• The key to realizing the main goal of fast and simple crash recov ery
in NFS is in the design of a stateless protocol. After a crash, the
server can quickly restart and begin serving requests again ; clients
just retry requests until they succeed.
• Making requests idempotent is a central aspect of the NFS protocol.
An operation is idempotent when the effect of performing it multi-
ple times is equivalent to performing it once. In NFS, idempotenc y
enables client retry without worry , and uniﬁes client lost-mes sage
retransmission and how the client handles server crashes.
• Performance concerns dictate the need for client-side caching and
write buffering, but introduces a cache consistency problem .
• NFS implementations provide an engineering solution to cache
consistency through multiple means: a ﬂush-on-close (close-to-
open) approach ensures that when a ﬁle is closed, its contents are
forced to the server, enabling other clients to observe the upda tes
to it. An attribute cache reduces the frequency of checking wi th the
server whether a ﬁle has changed (via GETATTR requests).
• NFS servers must commit writes to persistent media before ret urn-
ing success; otherwise, data loss can arise.
• To support NFS integration into the operating system, Sun intro-
duced the VFS/Vnode interface, enabling multiple ﬁle system im-
plementations to coexist in the same operating system.
potency of operations is essential; because a client can safely r eplay a
failed operation, it is OK to do so whether or not the server has exe cuted
the request.
We also have seen how the introduction of caching into a multiple-
client, single-server system can complicate things. In part icular, the sys-
tem must resolve the cache consistency problem in order to behave rea-
sonably; however, NFS does so in a slightly ad hoc fashion which can
occasionally result in observably weird behavior. Finally , we s aw how
server caching can be tricky: writes to the server must be forc ed to stable
storage before returning success (otherwise data can be lost).
We haven’t talked about other issues which are certainly releva nt, no-
tably security . Security in early NFS implementations was rem arkably
lax; it was rather easy for any user on a client to masquerade as ot her
users and thus gain access to virtually any ﬁle. Subsequent in tegration
with more serious authentication services (e.g., Kerberos [NT9 4]) have
addressed these obvious deﬁciencies.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

SUN’ S NETWORK FILE SYSTEM (NFS) 17
References
[AKW88] “The AWK Programming Language” by Alfred V . Aho, Brian W. Kerni ghan, Peter
J. Weinberger. Pearson, 1988 (1st edition). A concise, wonderful book about awk. We once had the
pleasure of meeting Peter Weinberger; when he introduced himself, he said “I’m Peter Weinberger, you
know, the ’W’ in awk?” As huge awk fans, this was a moment to savor. One of us (Remzi ) then said,
“I love awk! I particularly love the book, which makes everything so wonderful ly clear.” Weinberger
replied (crestfallen), “Oh, Kernighan wrote the book.”
[C00] “NFS Illustrated” by Brent Callaghan. Addison-Wesley Profess ional Computing Series,
2000. A great NFS reference; incredibly thorough and detailed per the protocol i tself.
[ES03] “New NFS Tracing Tools and Techniques for System Analysis” by Da niel Ellard and
Margo Seltzer. LISA ’03, San Diego, California. An intricate, careful analysis of NFS done via
passive tracing. By simply monitoring network trafﬁc, the authors show how to de rive a vast amount
of ﬁle system understanding.
[HLM94] “File System Design for an NFS File Server Appliance” by Da ve Hitz, James Lau,
Michael Malcolm. USENIX Winter 1994. San Francisco, California, 1994. Hitz et al. were greatly
inﬂuenced by previous work on log-structured ﬁle systems.
[K86] “Vnodes: An Architecture for Multiple File System Types in Sun UNIX ” by Steve R.
Kleiman. USENIX Summer ’86, Atlanta, Georgia. This paper shows how to build a ﬂexible ﬁle
system architecture into an operating system, enabling multiple differe nt ﬁle system implementations
to coexist. Now used in virtually every modern operating system in some form .
[NT94] “Kerberos: An Authentication Service for Computer Networks ” by B. Clifford Neu-
man, Theodore Ts’o. IEEE Communications, 32(9):33-38, September 199 4. Kerberos is an early
and hugely inﬂuential authentication service. We probably should write a b ook chapter about it some-
time...
[O91] “The Role of Distributed State” by John K. Ousterhout. 1991. Ava ilable at this site:
ftp://ftp.cs.berkeley.edu/ucb/sprite/papers/state.ps. A rarely referenced dis-
cussion of distributed state; a broader perspective on the problems and chall enges.
[P+94] “NFS V ersion 3: Design and Implementation” by Brian Pawlows ki, Chet Juszczak, Peter
Staubach, Carl Smith, Diane Lebel, Dave Hitz. USENIX Summer 1994 , pages 137-152. The small
modiﬁcations that underlie NFS version 3.
[P+00] “The NFS version 4 protocol” by Brian Pawlowski, David Noveck , David Robinson,
Robert Thurlow. 2nd International System Administration and Networking Conference (SANE
2000). Undoubtedly the most literary paper on NFS ever written.
[RO91] “The Design and Implementation of the Log-structured File Syst em” by Mendel Rosen-
blum, John Ousterhout. Symposium on Operating Systems Principles (SOSP), 1991. LFS again.
No, you can never get enough LFS.
[S86] “The Sun Network File System: Design, Implementation and Exp erience” by Russel
Sandberg. USENIX Summer 1986. The original NFS paper; though a bit of a challenging read,
it is worthwhile to see the source of these wonderful ideas.
[Sun89] “NFS: Network File System Protocol Speciﬁcation” by Sun Micro systems, Inc. Request
for Comments: 1094, March 1989. Available: http://www.ietf.org/rfc/rfc1094.txt.
The dreaded speciﬁcation; read it if you must, i.e., you are getting paid to r ead it. Hopefully, paid a lot.
Cash money!
[V72] “La Begueule” by Francois-Marie Arouet a.k.a. V oltaire. Pub lished in 1772. Voltaire said
a number of clever things, this being but one example. For example, Vol taire also said “If you have two
religions in your land, the two will cut each other’s throats; but if you have th irty religions, they will
dwell in peace.” What do you say to that, Democrats and Republicans?
© 2008–25, A RPACI -D USSEAU THREE
EASY
PIECES

18 S UN’ S NETWORK FILE SYSTEM (NFS)
Homework (Measurement)
In this homework, you’ll do a little bit of NFS trace analysis using real
traces. The source of these traces is Ellard and Seltzer’s effort [ ES03].
Make sure to read the related README and download the relevant t ar-
ball from the OSTEP homework page (as usual) before starting. One t ool
that might be fun to use during this analysis is the awk program ming
language [AKW88].
Questions
1. A ﬁrst question for your trace analysis: using the timestamps found
in the ﬁrst column, determine the period of time the traces were
taken from. How long is the period? What day/week/month/year
was it? (does this match the hint given in the ﬁle name?) Hint: U se
the tools head -1 and tail -1 to extract the ﬁrst and last lines of
the ﬁle, and do the calculation.
2. Now, let’s do some operation counts. How many of each type of op-
eration occur in the trace? Sort these by frequency; which operati on
is most frequent? Does NFS live up to its reputation?
3. Now let’s look at some particular operations in more detail. For
example, the GETATTR request returns a lot of information about
ﬁles, including which user ID the request is being performed f or,
the size of the ﬁle, and so forth. Make a distribution of ﬁle sizes
accessed within the trace; what is the average ﬁle size? Also, how
many different users access ﬁles in the trace? Do a few users d om-
inate trafﬁc, or is it more spread out? What other interesting inf or-
mation is found within GETATTR replies?
4. You can also look at requests to a given ﬁle and determine how
ﬁles are being accessed. For example, is a given ﬁle being read or
written sequentially? Or randomly? Look at the details of READ
and WRITE requests/replies to compute the answer.
5. Trafﬁc comes from many machines and goes to one server (in this
trace). Compute a trafﬁc matrix, which shows how many different
clients there are in the trace, and how many requests/replies go to
each. Do a few machines dominate, or is it more evenly balanced?
6. The timing information, and the per-request/reply unique I D, should
allow you to compute the latency for a given request. Compute the
latencies of all request/reply pairs, and plot them as a distri bution.
What is the average? Maximum? Minimum?
7. Sometimes requests are retried, as the request or its reply cou ld be
lost or dropped. Can you ﬁnd any evidence of such retrying in the
trace sample?
8. There are many other questions you could answer through more
analysis. What questions do you think are important? Suggest
them to us, and perhaps we’ll add them here!
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG
