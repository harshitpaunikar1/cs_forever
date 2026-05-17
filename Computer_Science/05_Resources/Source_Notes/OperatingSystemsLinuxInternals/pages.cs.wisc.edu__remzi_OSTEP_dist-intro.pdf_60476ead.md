Title: dist-intro.pdf
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/dist-intro.pdf
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:55:14+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

48
Distributed Systems
Distributed systems have changed the face of the world. When you r web
browser connects to a web server somewhere else on the planet, it i s par-
ticipating in what seems to be a simple form of a client/server distributed
system. When you contact a modern web service such as Google or Face-
book, you are not just interacting with a single machine, however; be-
hind the scenes, these complex services are built from a large c ollection
(i.e., thousands) of machines, each of which cooperate to provide t he par-
ticular service of the site. Thus, it should be clear what makes studying
distributed systems interesting. Indeed, it is worthy of an en tire class;
here, we just introduce a few of the major topics.
A number of new challenges arise when building a distributed system.
The major one we focus on is failure; machines, disks, networks, and
software all fail from time to time, as we do not (and likely , will never)
know how to build “perfect” components and systems. However, when
we build a modern web service, we’d like it to appear to clients a s if it
never fails; how can we accomplish this task?
THE CRUX :
HOW TO BUILD SYSTEMS THAT WORK WHEN COMPONENTS FAIL
How can we build a working system out of parts that don’t work correctly
all the time? The basic question should remind you of some of the topic s
we discussed in RAID storage arrays; however, the problems here tend
to be more complex, as are the solutions.
Interestingly , while failure is a central challenge in const ructing dis-
tributed systems, it also represents an opportunity . Yes, mac hines fail;
but the mere fact that a machine fails does not imply the entire s ystem
must fail. By collecting together a set of machines, we can build a system
that appears to rarely fail, despite the fact that its componen ts fail regu-
larly . This reality is the central beauty and value of distrib uted systems,
and why they underlie virtually every modern web service you us e, in-
cluding Google, Facebook, etc.
1

2 D ISTRIBUTED SYSTEMS
TIP : C OMMUNICATION IS INHERENTLY UNRELIABLE
In virtually all circumstances, it is good to view communication as a
fundamentally unreliable activity . Bit corruption, down or non- working
links and machines, and lack of buffer space for incoming packet s all lead
to the same result: packets sometimes do not reach their destin ation. To
build reliable services atop such unreliable networks, we mus t consider
techniques that can cope with packet loss.
Other important issues exist as well. System performance is often crit-
ical; with a network connecting our distributed system together , system
designers must often think carefully about how to accomplish the ir given
tasks, trying to reduce the number of messages sent and furthe r make
communication as efﬁcient (low latency , high bandwidth) as possible.
Finally ,security is also a necessary consideration. When connecting
to a remote site, having some assurance that the remote party is w ho
they say they are becomes a central problem. Further, ensuring that third
parties cannot monitor or alter an on-going communication between tw o
others is also a challenge.
In this introduction, we’ll cover the most basic aspect that is new in
a distributed system: communication. Namely , how should machines
within a distributed system communicate with one another? We’ll start
with the most basic primitives available, messages, and build a few higher-
level primitives on top of them. As we said above, failure will be a central
focus: how should communication layers handle failures?
48.1 Communication Basics
The central tenet of modern networking is that communication is fu n-
damentally unreliable. Whether in the wide-area Internet, or a local-area
high-speed network such as Inﬁniband, packets are regularly lost, cor-
rupted, or otherwise do not reach their destination.
There are a multitude of causes for packet loss or corruption. Some-
times, during transmission, some bits get ﬂipped due to electrical or other
similar problems. Sometimes, an element in the system, such as a net-
work link or packet router or even the remote host, are somehow dam-
aged or otherwise not working correctly; network cables do acciden tally
get severed, at least sometimes.
More fundamental however is packet loss due to lack of buffering
within a network switch, router, or endpoint. Speciﬁcally , even i f we
could guarantee that all links worked correctly , and that all th e compo-
nents in the system (switches, routers, end hosts) were up and r unning as
expected, loss is still possible, for the following reason. Imagin e a packet
arrives at a router; for the packet to be processed, it must be pla ced in
memory somewhere within the router. If many such packets arrive at
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DISTRIBUTED SYSTEMS 3
// client code
int main(int argc, char *argv[]) {
int sd = UDP_Open(20000);
struct sockaddr_in addrSnd, addrRcv;
int rc = UDP_FillSockAddr(&addrSnd, "cs.wisc.edu", 10000 );
char message[BUFFER_SIZE];
sprintf(message, "hello world");
rc = UDP_Write(sd, &addrSnd, message, BUFFER_SIZE);
if (rc > 0)
int rc = UDP_Read(sd, &addrRcv, message, BUFFER_SIZE);
return 0;
}
// server code
int main(int argc, char *argv[]) {
int sd = UDP_Open(10000);
assert(sd > -1);
while (1) {
struct sockaddr_in addr;
char message[BUFFER_SIZE];
int rc = UDP_Read(sd, &addr, message, BUFFER_SIZE);
if (rc > 0) {
char reply[BUFFER_SIZE];
sprintf(reply, "goodbye world");
rc = UDP_Write(sd, &addr, reply, BUFFER_SIZE);
}
}
return 0;
}
Figure 48.1: Example UDP Code ( client.c, server.c)
once, it is possible that the memory within the router cannot accomm o-
date all of the packets. The only choice the router has at that point is
to drop one or more of the packets. This same behavior occurs at end
hosts as well; when you send a large number of messages to a single ma-
chine, the machine’s resources can easily become overwhelmed, a nd thus
packet loss again arises.
Thus, packet loss is fundamental in networking. The question th us
becomes: how should we deal with it?
48.2 Unreliable Communication Layers
One simple way is this: we don’t deal with it. Because some appli-
cations know how to deal with packet loss, it is sometimes useful to let
them communicate with a basic unreliable messaging layer, an example
of the end-to-end argument one often hears about (see the Aside at end
of chapter). One excellent example of such an unreliable layer is found
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

4 D ISTRIBUTED SYSTEMS
int UDP_Open(int port) {
int sd;
if ((sd = socket(AF_INET, SOCK_DGRAM, 0)) == -1)
return -1;
struct sockaddr_in myaddr;
bzero(&myaddr, sizeof(myaddr));
myaddr.sin_family = AF_INET;
myaddr.sin_port = htons(port);
myaddr.sin_addr.s_addr = INADDR_ANY;
if (bind(sd, (struct sockaddr *) &myaddr,
sizeof(myaddr)) == -1) {
close(sd);
return -1;
}
return sd;
}
int UDP_FillSockAddr(struct sockaddr_in *addr,
char *hostname, int port) {
bzero(addr, sizeof(struct sockaddr_in));
addr->sin_family = AF_INET; // host byte order
addr->sin_port = htons(port); // network byte order
struct in_addr *in_addr;
struct hostent *host_entry;
if ((host_entry = gethostbyname(hostname)) == NULL)
return -1;
in_addr = (struct in_addr *) host_entry->h_addr;
addr->sin_addr = *in_addr;
return 0;
}
int UDP_Write(int sd, struct sockaddr_in *addr,
char *buffer, int n) {
int addr_len = sizeof(struct sockaddr_in);
return sendto(sd, buffer, n, 0, (struct sockaddr *)
addr, addr_len);
}
int UDP_Read(int sd, struct sockaddr_in *addr,
char *buffer, int n) {
int len = sizeof(struct sockaddr_in);
return recvfrom(sd, buffer, n, 0, (struct sockaddr *)
addr, (socklen_t *) &len);
}
Figure 48.2: A Simple UDP Library ( udp.c)
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DISTRIBUTED SYSTEMS 5
TIP : U SE CHECKSUMS FOR INTEGRITY
Checksums are a commonly-used method to detect corruption quickl y
and effectively in modern systems. A simple checksum is addit ion: just
sum up the bytes of a chunk of data; of course, many other more sophis-
ticated checksums have been created, including basic cycli c redundancy
codes (CRCs), the Fletcher checksum, and many others [MK09].
In networking, checksums are used as follows. Before sending a me ssage
from one machine to another, compute a checksum over the bytes of the
message. Then send both the message and the checksum to the des ti-
nation. At the destination, the receiver computes a checksum ove r the
incoming message as well; if this computed checksum matches th e sent
checksum, the receiver can feel some assurance that the data l ikely did
not get corrupted during transmission.
Checksums can be evaluated along a number of different axes. Ef fective-
ness is one primary consideration: does a change in the data lead t o a
change in the checksum? The stronger the checksum, the harder it is for
changes in the data to go unnoticed. Performance is the other imp ortant
criterion: how costly is the checksum to compute? Unfortunately , effec-
tiveness and performance are often at odds, meaning that checks ums of
high quality are often expensive to compute. Life, again, isn’t perfect.
in the UDP/IP networking stack available today on virtually all modern
systems. To use UDP , a process uses the sockets API in order to create a
communication endpoint; processes on other machines (or on the same
machine) send UDP datagrams to the original process (a datagram is a
ﬁxed-sized message up to some max size).
Figures 48.1 and 48.2 show a simple client and server built on top of
UDP/IP . The client can send a message to the server, which then responds
with a reply . With this small amount of code, you have all you need to
begin building distributed systems!
UDP is a great example of an unreliable communication layer. If y ou
use it, you will encounter situations where packets get lost (drop ped) and
thus do not reach their destination; the sender is never thus in formed of
the loss. However, that does not mean that UDP does not guard against
any failures at all. For example, UDP includes a checksum to detect some
forms of packet corruption.
However, because many applications simply want to send data to a
destination and not worry about packet loss, we need more. Speciﬁcal ly ,
we need reliable communication on top of an unreliable network.
48.3 Reliable Communication Layers
To build a reliable communication layer, we need some new mech-
anisms and techniques to handle packet loss. Let us consider a s imple
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

6 D ISTRIBUTED SYSTEMS
Sender
[send message]
Receiver
[receive message]
[send ack]
[receive ack]
Figure 48.3: Message Plus Acknowledgment
Sender
[send message;
keep copy;
set timer]
Receiver
...
(waiting for ack)
...
[timer goes off;
set timer/retry]
[receive message]
[send ack]
[receive ack;
delete copy/timer off]
Figure 48.4: Message Plus Acknowledgment: Dropped Request
example in which a client is sending a message to a server over a n unreli-
able connection. The ﬁrst question we must answer: how does the sen der
know that the receiver has actually received the message?
The technique that we will use is known as an acknowledgment, or
ack for short. The idea is simple: the sender sends a message to the r e-
ceiver; the receiver then sends a short message back to acknowledge its
receipt. Figure 48.3 depicts the process.
When the sender receives an acknowledgment of the message, it c an
then rest assured that the receiver did indeed receive the ori ginal mes-
sage. However, what should the sender do if it does not receive an a c-
knowledgment?
To handle this case, we need an additional mechanism, known as a
timeout. When the sender sends a message, the sender now sets a timer
to go off after some period of time. If, in that time, no acknowledgm ent
has been received, the sender concludes that the message has b een lost.
The sender then simply performs a retry of the send, sending the same
message again with hopes that this time, it will get through. For this
approach to work, the sender must keep a copy of the message around,
in case it needs to send it again. The combination of the timeout an d
the retry have led some to call the approach timeout/retry; pretty clever
crowd, those networking types, no? Figure 48.4 shows an example.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DISTRIBUTED SYSTEMS 7
Sender
[send message;
keep copy;
set timer]
Receiver
[receive message]
[send ack]
...
(waiting for ack)
...
[timer goes off;
set timer/retry]
[receive message]
[send ack]
[receive ack;
delete copy/timer off]
Figure 48.5: Message Plus Acknowledgment: Dropped Reply
Unfortunately , timeout/retry in this form is not quite enough. Fi gure
48.5 shows an example of packet loss which could lead to trouble. In this
example, it is not the original message that gets lost, but the ac knowledg-
ment. From the perspective of the sender, the situation seems th e same:
no ack was received, and thus a timeout and retry are in order. Bu t from
the perspective of the receiver, it is quite different: now the same message
has been received twice! While there may be cases where this i s OK, in
general it is not; imagine what would happen when you are downloading
a ﬁle and extra packets are repeated inside the download. Thus, when we
are aiming for a reliable message layer, we also usually want to guarantee
that each message is received exactly once by the receiver.
To enable the receiver to detect duplicate message transmis sion, the
sender has to identify each message in some unique way , and thereceiver
needs some way to track whether it has already seen each messag e be-
fore. When the receiver sees a duplicate transmission, it simp ly acks the
message, but (critically) does not pass the message to the application that
receives the data. Thus, the sender receives the ack but the m essage is not
received twice, preserving the exactly-once semantics ment ioned above.
There are myriad ways to detect duplicate messages. For examp le, the
sender could generate a unique ID for each message; the receive r could
track every ID it has ever seen. This approach could work, but it i s pro-
hibitively costly , requiring unbounded memory to track all IDs.
A simpler approach, requiring little memory , solves this problem, and
the mechanism is known as a sequence counter. With a sequence counter,
the sender and receiver agree upon a start value (e.g., 1) for a c ounter
that each side will maintain. Whenever a message is sent, the current
value of the counter is sent along with the message; this counter v alue
(N ) serves as an ID for the message. After the message is sent, the sender
then increments the value (to N + 1).
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

8 D ISTRIBUTED SYSTEMS
TIP : B E CAREFUL SETTING THE TIMEOUT VALUE
As you can probably guess from the discussion, setting the timeout value
correctly is an important aspect of using timeouts to retry messa ge sends.
If the timeout is too small, the sender will re-send messages ne edlessly ,
thus wasting CPU time on the sender and network resources. If the time-
out is too large, the sender waits too long to re-send and thus perc eived
performance at the sender is reduced. The “right” value, from t he per-
spective of a single client and server, is thus to wait just long enough to
detect packet loss but no longer.
However, there are often more than just a single client and serve r in a
distributed system, as we will see in future chapters. In a sc enario with
many clients sending to a single server, packet loss at the ser ver may be
an indicator that the server is overloaded. If true, clients mig ht retry in
a different adaptive manner; for example, after the ﬁrst time out, a client
might increase its timeout value to a higher amount, perhaps tw ice as
high as the original value. Such an exponential back-off scheme, pio-
neered in the early Aloha network and adopted in early Ethernet [ A70],
avoids situations where resources are being overloaded by an exce ss of
re-sends. Robust systems strive to avoid overload of this nature.
The receiver uses its counter value as the expected value for th e ID
of the incoming message from that sender. If the ID of a received me s-
sage (N ) matches the receiver’s counter (also N ), it acks the message and
passes it up to the application; in this case, the receiver conc ludes this
is the ﬁrst time this message has been received. The receiver then incre-
ments its counter (to N + 1), and waits for the next message.
If the ack is lost, the sender will timeout and re-send message N . This
time, the receiver’s counter is higher ( N + 1), and thus the receiver knows
it has already received this message. Thus it acks the messag e but does
not pass it up to the application. In this simple manner, sequence counters
can be used to avoid duplicates.
The most commonly used reliable communication layer is known as
TCP/IP, or just TCP for short. TCP has a great deal more sophistication
than we describe above, including machinery to handle congest ion in the
network [VJ88], multiple outstanding requests, and hundreds of other
small tweaks and optimizations. Read more about it if you’re curious ;
better yet, take a networking course and learn that material we ll.
48.4 Communication Abstractions
Given a basic messaging layer, we now approach the next question
in this chapter: what abstraction of communication should we use w hen
building a distributed system?
The systems community developed a number of approaches over the
years. One body of work took OS abstractions and extended them to
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DISTRIBUTED SYSTEMS 9
operate in a distributed environment. For example, distributed shared
memory (DSM) systems enable processes on different machines to share
a large, virtual address space [LH89]. This abstraction turn s a distributed
computation into something that looks like a multi-threaded appl ication;
the only difference is that these threads run on different mach ines instead
of different processors within the same machine.
The way most DSM systems work is through the virtual memory sys-
tem of the OS. When a page is accessed on one machine, two things can
happen. In the ﬁrst (best) case, the page is already local on the machine,
and thus the data is fetched quickly . In the second case, the pa ge is cur-
rently on some other machine. A page fault occurs, and the page fau lt
handler sends a message to some other machine to fetch the page, install
it in the page table of the requesting process, and continue exec ution.
This approach is not widely in use today for a number of reasons. The
largest problem for DSM is how it handles failure. Imagine, for exa mple,
if a machine fails; what happens to the pages on that machine? W hat if
the data structures of the distributed computation are spread a cross the
entire address space? In this case, parts of these data struct ures would
suddenly become unavailable. Dealing with failure when part s of your
address space go missing is hard; imagine a linked list where a “next”
pointer points into a portion of the address space that is gone. Yike s!
A further problem is performance. One usually assumes, when wr it-
ing code, that access to memory is cheap. In DSM systems, some acce sses
are inexpensive, but others cause page faults and expensive f etches from
remote machines. Thus, programmers of such DSM systems had to be
very careful to organize computations such that almost no communi ca-
tion occurred at all, defeating much of the point of such an approach .
Though much research was performed in this space, there was lit tle prac-
tical impact; nobody builds reliable distributed systems using DSM today .
48.5 Remote Procedure Call (RPC)
While OS abstractions turned out to be a poor choice for building dis -
tributed systems, programming language (PL) abstractions ma ke much
more sense. The most dominant abstraction is based on the idea of a re-
mote procedure call , or RPC for short [BN84] 1.
Remote procedure call packages all have a simple goal: to make th e
process of executing code on a remote machine as simple and straigh t-
forward as calling a local function. Thus, to a client, a procedur e call is
made, and some time later, the results are returned. The serve r simply
deﬁnes some routines that it wishes to export. The rest of the magi c is
handled by the RPC system, which in general has two pieces: a stub gen-
erator (sometimes called a protocol compiler), and the run-time library.
We’ll now take a look at each of these pieces in more detail.
1In modern programming languages, we might instead say remote method invocation
(RMI), but who likes these languages anyhow, with all of their fancy objects?
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

10 D ISTRIBUTED SYSTEMS
Stub Generator
The stub generator’s job is simple: to remove some of the pain of packi ng
function arguments and results into messages by automating it . Numer-
ous beneﬁts arise: one avoids, by design, the simple mistakes th at occur
in writing such code by hand; further, a stub compiler can perha ps opti-
mize such code and thus improve performance.
The input to such a compiler is simply the set of calls a server wi shes
to export to clients. Conceptually , it could be something as simple as this:
interface {
int func1(int arg1);
int func2(int arg1, int arg2);
};
The stub generator takes an interface like this and generates a few dif-
ferent pieces of code. For the client, a client stub is generated, which
contains each of the functions speciﬁed in the interface; a clie nt program
wishing to use this RPC service would link with this client stu b and call
into it in order to make RPCs.
Internally , each of these functions in the client stub do all of t he work
needed to perform the remote procedure call. To the client, the c ode just
appears as a function call (e.g., the client calls func1(x)); internally , the
code in the client stub for func1() does this:
• Create a message buffer. A message buffer is usually just a con-
tiguous array of bytes of some size.
• Pack the needed information into the message buffer. This infor-
mation includes some kind of identiﬁer for the function to be called,
as well as all of the arguments that the function needs (e.g., in our
example above, one integer for func1). The process of putting all
of this information into a single contiguous buffer is sometimes re -
ferred to as the marshaling of arguments or the serialization of the
message.
• Send the message to the destination RPC server. The communi-
cation with the RPC server, and all of the details required to ma ke
it operate correctly , are handled by the RPC run-time library , de-
scribed further below.
• Wait for the reply. Because function calls are usually synchronous,
the call will wait for its completion.
• Unpack return code and other arguments. If the function just re-
turns a single return code, this process is straightforward; how ever,
more complex functions might return more complex results (e.g., a
list), and thus the stub might need to unpack those as well. Thi s
step is also known as unmarshaling or deserialization.
• Return to the caller. Finally , just return from the client stub back
into the client code.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DISTRIBUTED SYSTEMS 11
For the server, code is also generated. The steps taken on the ser ver
are as follows:
• Unpack the message. This step, called unmarshaling or deserial-
ization, takes the information out of the incoming message. The
function identiﬁer and arguments are extracted.
• Call into the actual function. Finally! We have reached the point
where the remote function is actually executed. The RPC runtim e
calls into the function speciﬁed by the ID and passes in the des ired
arguments.
• Package the results. The return argument(s) are marshaled back
into a single reply buffer.
• Send the reply. The reply is ﬁnally sent to the caller.
There are a few other important issues to consider in a stub compil er.
The ﬁrst is complex arguments, i.e., how does one package and send
a complex data structure? For example, when one calls the write()
system call, one passes in three arguments: an integer ﬁle des criptor, a
pointer to a buffer, and a size indicating how many bytes (start ing at the
pointer) are to be written. If an RPC package is passed a pointer , it needs
to be able to ﬁgure out how to interpret that pointer, and perform t he
correct action. Usually this is accomplished through either wel l-known
types (e.g., a buffer
t that is used to pass chunks of data given a size,
which the RPC compiler understands), or by annotating the data s truc-
tures with more information, enabling the compiler to know which b ytes
need to be serialized.
Another important issue is the organization of the server with reg ards
to concurrency . A simple server just waits for requests in a sim ple loop,
and handles each request one at a time. However, as you might have
guessed, this can be grossly inefﬁcient; if one RPC call blocks ( e.g., on
I/O), server resources are wasted. Thus, most servers are const ructed in
some sort of concurrent fashion. A common organization is a thread pool.
In this organization, a ﬁnite set of threads are created when the server
starts; when a message arrives, it is dispatched to one of these worker
threads, which then does the work of the RPC call, eventually rep lying;
during this time, a main thread keeps receiving other request s, and per-
haps dispatching them to other workers. Such an organization enab les
concurrent execution within the server, thus increasing its u tilization; the
standard costs arise as well, mostly in programming complexity , as the
RPC calls may now need to use locks and other synchronization primi -
tives in order to ensure their correct operation.
Run-Time Library
The run-time library handles much of the heavy lifting in an RP C system;
most performance and reliability issues are handled herein. W e’ll now
discuss some of the major challenges in building such a run-time layer.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

12 D ISTRIBUTED SYSTEMS
One of the ﬁrst challenges we must overcome is how to locate a re-
mote service. This problem, of naming, is a common one in distributed
systems, and in some sense goes beyond the scope of our current discu s-
sion. The simplest of approaches build on existing naming system s, e.g.,
hostnames and port numbers provided by current internet protocols . In
such a system, the client must know the hostname or IP address of th e
machine running the desired RPC service, as well as the port nu mber it is
using (a port number is just a way of identifying a particular com munica-
tion activity taking place on a machine, allowing multiple communication
channels at once). The protocol suite must then provide a mechanis m to
route packets to a particular address from any other machine in t he sys-
tem. For a good discussion of naming, you’ll have to look elsewhere, e.g .,
read about DNS and name resolution on the Internet, or better yet ju st
read the excellent chapter in Saltzer and Kaashoek’s book [SK09].
Once a client knows which server it should talk to for a particula r re-
mote service, the next question is which transport-level protocol should
RPC be built upon. Speciﬁcally , should the RPC system use a reliable pro-
tocol such as TCP/IP , or be built upon an unreliable communication layer
such as UDP/IP?
Naively the choice would seem easy: clearly we would like for a re-
quest to be reliably delivered to the remote server, and clear ly we would
like to reliably receive a reply . Thus we should choose the relia ble trans-
port protocol such as TCP , right?
Unfortunately , building RPC on top of a reliable communication layer
can lead to a major inefﬁciency in performance. Recall from the d iscus-
sion above how reliable communication layers work: with acknowledg -
ments plus timeout/retry . Thus, when the client sends an RPC r equest
to the server, the server responds with an acknowledgment so th at the
caller knows the request was received. Similarly , when the ser ver sends
the reply to the client, the client acks it so that the server k nows it was
received. By building a request/response protocol (such as RPC) on top
of a reliable communication layer, two “extra” messages are sen t.
For this reason, many RPC packages are built on top of unreliable com-
munication layers, such as UDP . Doing so enables a more efﬁcient RPC
layer, but does add the responsibility of providing reliability to the RPC
system. The RPC layer achieves the desired level of responsibi lity by us-
ing timeout/retry and acknowledgments much like we described above.
By using some form of sequence numbering, the communication layer
can guarantee that each RPC takes place exactly once (in the ca se of no
failure), or at most once (in the case where failure arises).
Other Issues
There are some other issues an RPC run-time must handle as well. For
example, what happens when a remote call takes a long time to com-
plete? Given our timeout machinery , a long-running remote call m ight
appear as a failure to a client, thus triggering a retry , and t hus the need
for some care here. One solution is to use an explicit acknowledgme nt
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DISTRIBUTED SYSTEMS 13
Aside: T HE END -TO-E ND ARGUMENT
The end-to-end argument makes the case that the highest level in a sys-
tem, i.e., usually the application at “the end”, is ultimatel y the only lo-
cale within a layered system where certain functionality can truly be im-
plemented. In their landmark paper [SRC84], Saltzer et al. arg ue this
through an excellent example: reliable ﬁle transfer between two ma-
chines. If you want to transfer a ﬁle from machine A to machine B, and
make sure that the bytes that end up on B are exactly the same as those
that began on A, you must have an “end-to-end” check of this; lower-
level reliable machinery , e.g., in the network or disk, provide s no such
guarantee.
The contrast is an approach which tries to solve the reliable-ﬁl e-transfer
problem by adding reliability to lower layers of the system. For e xample,
say we build a reliable communication protocol and use it to build ou r
reliable ﬁle transfer. The communication protocol guarantees th at every
byte sent by a sender will be received in order by the receiver, say us-
ing timeout/retry , acknowledgments, and sequence numbers. U nfortu-
nately , using such a protocol does not a reliable ﬁle transfer make ; imag-
ine the bytes getting corrupted in sender memory before the commu ni-
cation even takes place, or something bad happening when the rec eiver
writes the data to disk. In those cases, even though the bytes we re deliv-
ered reliably across the network, our ﬁle transfer was ultimate ly not reli-
able. To build a reliable ﬁle transfer, one must include end-t o-end checks
of reliability , e.g., after the entire transfer is complete, r ead back the ﬁle
on the receiver disk, compute a checksum, and compare that check sum
to that of the ﬁle on the sender.
The corollary to this maxim is that sometimes having lower layers pro-
vide extra functionality can indeed improve system performanc e or oth-
erwise optimize a system. Thus, you should not rule out having such
machinery at a lower-level in a system; rather, you should caref ully con-
sider the utility of such machinery , given its eventual usage in an overall
system or application.
(from the receiver to sender) when the reply isn’t immediately generated;
this lets the client know the server received the request. The n, after some
time has passed, the client can periodically ask whether the s erver is still
working on the request; if the server keeps saying “yes”, the cl ient should
be happy and continue to wait (after all, sometimes a procedure c all can
take a long time to ﬁnish executing).
The run-time must also handle procedure calls with large argu ments,
larger than what can ﬁt into a single packet. Some lower-level ne twork
protocols provide such sender-side fragmentation (of larger packets into
a set of smaller ones) and receiver-side reassembly (of smaller parts into
one larger logical whole); if not, the RPC run-time may have to implement
such functionality itself. See Birrell and Nelson’s paper for det ails [BN84].
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

14 D ISTRIBUTED SYSTEMS
One issue that many systems handle is that of byte ordering. As you
may know, some machines store values in what is known as big endian
ordering, whereas others use little endian ordering. Big endian stores
bytes (say , of an integer) from most signiﬁcant to least signiﬁc ant bits,
much like Arabic numerals; little endian does the opposite. Both are
equally valid ways of storing numeric information; the question h ere is
how to communicate between machines of different endianness.
RPC packages often handle this by providing a well-deﬁned endi -
anness within their message formats. In Sun’s RPC package, the XDR
(eXternal Data Representation ) layer provides this functionality . If the
machine sending or receiving a message matches the endiannes s of XDR,
messages are just sent and received as expected. If, however, the machine
communicating has a different endianness, each piece of inform ation in
the message must be converted. Thus, the difference in endian ness can
have a small performance cost.
A ﬁnal issue is whether to expose the asynchronous nature of com-
munication to clients, thus enabling some performance optimiza tions.
Speciﬁcally , typical RPCs are made synchronously, i.e., when a client
issues the procedure call, it must wait for the procedure call to return
before continuing. Because this wait can be long, and because th e client
may have other work it could be doing, some RPC packages enable you
to invoke an RPC asynchronously. When an asynchronous RPC is is-
sued, the RPC package sends the request and returns immediat ely; the
client is then free to do other work, such as call other RPCs or other use-
ful computation. The client at some point will want to see the resu lts of
the asynchronous RPC; it thus calls back into the RPC layer, tel ling it to
wait for outstanding RPCs to complete, at which point return argu ments
can be accessed.
48.6 Summary
We have seen the introduction of a new topic, distributed systems, and
its major issue: how to handle failure which is now a commonplace event.
As they say inside of Google, when you have just your desktop machine ,
failure is rare; when you’re in a data center with thousands of mac hines,
failure is happening all the time. The key to any distributed system is
how you deal with that failure.
We have also seen that communication forms the heart of any dis-
tributed system. A common abstraction of that communication is foun d
in remote procedure call (RPC), which enables clients to make r emote
calls on servers; the RPC package handles all of the gory details , includ-
ing timeout/retry and acknowledgment, in order to deliver a ser vice that
closely mirrors a local procedure call.
The best way to really understand an RPC package is of course to u se
one yourself. Sun’s RPC system, using the stub compiler rpcgen, is an
older one; Google’s gRPC and Apache Thrift are modern takes on the
same. Try one out, and see what all the fuss is about.
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DISTRIBUTED SYSTEMS 15
References
[A70] “The ALOHA System — Another Alternative for Computer Communicati ons” by Nor-
man Abramson. The 1970 Fall Joint Computer Conference. The ALOHA network pioneered some
basic concepts in networking, including exponential back-off and retransmit, which formed the basis for
communication in shared-bus Ethernet networks for years.
[BN84] “Implementing Remote Procedure Calls” by Andrew D. Birrell , Bruce Jay Nelson.
ACM TOCS, V olume 2:1, February 1984.The foundational RPC system upon which all others build.
Y es, another pioneering effort from our friends at Xerox P ARC.
[MK09] “The Effectiveness of Checksums for Embedded Control Networks” b y Theresa C.
Maxino and Philip J. Koopman. IEEE Transactions on Dependable and Secure Co mputing,
6:1, January ’09. A nice overview of basic checksum machinery and some performance and robu stness
comparisons between them.
[LH89] “Memory Coherence in Shared Virtual Memory Systems” by Kai Li and Paul Hudak.
ACM TOCS, 7:4, November 1989. The introduction of software-based shared memory via virtual
memory. An intriguing idea for sure, but not a lasting or good one in the end .
[SK09] “Principles of Computer System Design” by Jerome H. Saltzer and M. Frans Kaashoek.
Morgan-Kaufmann, 2009. An excellent book on systems, and a must for every bookshelf. One of the
few terriﬁc discussions on naming we’ve seen.
[SRC84] “End-To-End Arguments in System Design” by Jerome H. Saltzer , David P . Reed,
David D. Clark. ACM TOCS, 2:4, November 1984. A beautiful discussion of layering, abstraction,
and where functionality must ultimately reside in computer systems.
[VJ88] “Congestion Avoidance and Control” by Van Jacobson. SIGCOMM ’88 . A pioneering
paper on how clients should adjust to perceived network congestion; deﬁni tely one of the key pieces of
technology underlying the Internet, and a must read for anyone serious about s ystems, and for Van
Jacobson’s relatives because well relatives should read all of your papers.
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES

16 D ISTRIBUTED SYSTEMS
Homework (Code)
In this section, we’ll write some simple communication code to get
you familiar with the task of doing so. Have fun!
Questions
1. Using the code provided in the chapter, build a simple UDP-ba sed
server and client. The server should receive messages from the
client, and reply with an acknowledgment. In this ﬁrst attemp t,
do not add any retransmission or robustness (assume that commu-
nication works perfectly). Run this on a single machine for testi ng;
later, run it on two different machines.
2. Turn your code into a communication library . Speciﬁcally , make
your own API, with send and receive calls, as well as other API
calls as needed. Rewrite your client and server to use your libr ary
instead of raw socket calls.
3. Add reliable communication to your burgeoning communication li -
brary , in the form oftimeout/retry. Speciﬁcally , your library should
make a copy of any message that it is going to send. When sending
it, it should start a timer, so it can track how long it has been sin ce
the message was sent. On the receiver, the library should acknowl-
edge received messages. The client send should block when send-
ing, i.e., it should wait until the message has been acknowledg ed
before returning. It should also be willing to retry sending in def-
initely . The maximum message size should be that of the largest
single message you can send with UDP . Finally , be sure to perform
timeout/retry efﬁciently by putting the caller to sleep unti l either
an ack arrives or the transmission times out; do not spin and waste
the CPU!
4. Make your library more efﬁcient and feature-ﬁlled. First, a dd very-
large message transfer. Speciﬁcally , although the network limit max-
imum message size, your library should take a message of arbitra r-
ily large size and transfer it from client to server. The clien t should
transmit these large messages in pieces to the server; the server-side
library code should assemble received fragments into the conti gu-
ous whole, and pass the single large buffer to the waiting serve r
code.
5. Do the above again, but with high performance. Instead of send ing
each fragment one at a time, you should rapidly send many pieces,
thus allowing the network to be much more highly utilized. To do
so, carefully mark each piece of the transfer so that the re-ass embly
on the receiver side does not scramble the message.
6. A ﬁnal implementation challenge: asynchronous message send with
in-order delivery . That is, the client should be able to repeatedly call
send to send one message after the other; the receiver should call re-
ceive and get each message in order, reliably; many messages f rom
OPERATING
SYSTEMS
[V ERSION 1.10]
WWW.OSTEP .ORG

DISTRIBUTED SYSTEMS 17
the sender should be able to be in ﬂight concurrently . Also add a
sender-side call that enables a client to wait for all outstanding mes-
sages to be acknowledged.
7. Now, one more pain point: measurement. Measure the bandwidth
of each of your approaches; how much data can you transfer be-
tween two different machines, at what rate? Also measure lat ency:
for single packet send and acknowledgment, how quickly does it
ﬁnish? Finally , do your numbers look reasonable? What did you
expect? How can you better set your expectations so as to know if
there is a problem, or that your code is working well?
© 2008–23, A RPACI -D USSEAU THREE
EASY
PIECES
