Title: 6.5840 Spring 2026 Paper Questions
Mapped Topic: Distributed systems labs and schedule
Source URL: https://pdos.csail.mit.edu/6.5840/questions.html
Source Type: official_course
Trust Score: 97
Fetched At: 2026-04-17T07:00:39+00:00
Mapped From CSE.md Section: Part 1 / Part 2.E

# Content

For each paper, your assignment is two-fold. Before the start of lecture discussing the paper:

- Read the paper, and
- Submit your answer for each lecture's paper question.

Put your answer in `a.txt` and question in `q.txt`.
Submit both files via
[Gradescope](https://www.gradescope.com/courses/974763).

The assigned reading for today is not a paper, but
the [Online Go tutorial](http://tour.golang.org/). The assigned
"question" is the
[Crawler exercise](https://tour.golang.org/concurrency/10) in the
tutorial. Also, take a look at
Go's [RPC package](https://golang.org/pkg/net/rpc/), which you
will use in lab 1.

The GFS paper is a "classic" paper that describes one of the first distributed file systems for data-center applications such as large MapReduce jobs. It touches on many themes of 6.5840: parallel performance, fault tolerance, replication, and consistency. It is good systems paper with details from apps all the way to network successful.

GFS has been replaced by something called
[Colossus](https://cloud.google.com/blog/products/storage-data-transfer/a-peek-behind-colossus-googles-file-system),
with the same overall goals, but improvements in master performance
and fault-tolerance. In addition, many applications within Google have
switched to more database-like storage systems such as BigTable and
Spanner. However, much of the GFS design lives on in HDFS, the storage
system for the Hadoop open-source MapReduce.

**Question**:
Describe a sequence of events that would result in a client reading stale
data from the [Google File System](https://pdos.csail.mit.edu/papers/gfs.pdf).

How does [VM FT](https://pdos.csail.mit.edu/papers/vm-ft.pdf) handle network partitions? That
is, is it possible that if the primary and the backup end up in different
network partitions that the backup will become a primary too and the system
will run with two primaries?

Consider the following code from the "incorrect synchronization" examples:

var a string var done bool func setup() { a = "hello, world" done = true } func main() { go setup() for !done { } print(a) }

Using the synchronization mechanisms of your choice, fix this code so it is guaranteed to have the intended behavior according to the Go language specification. Explain why your modification works in terms of the happens-before relation.

[Paxos Made Simple](https://pdos.csail.mit.edu/papers/paxos-simple.pdf)
Suppose that the acceptors are *A*, *B*,
and *C*. *A* and *B* are also
proposers.
How does Paxos
ensure that the following sequence of events __can't__ happen?
What actually happens, and which value is ultimately chosen?

-
*A*sends prepare requests with proposal number 1, and gets positive responses from*A*,*B*, and*C*. -
*A*sendstoaccept(1, "X") *A*and*C*and gets positive responses from both. Because a majority accepted,*A*thinks that`"X"`has been chosen. However,*A*crashes before sending an`accept`to*B*. *B*sends prepare messages with proposal number 2, and gets positive responses from*B*and*C*.*B*sendsmessages toaccept(2, "Y") *B*and*C*and gets positive responses from both, so*B*thinks that`"Y"`has been chosen.

The Raft paper describes a consensus algorithm, including many details that are needed to build replication-state machine applications. The paper is also the topic of several of the 6.5840 labs. The important sections are 2, 5, 7, and 8.

The paper positions itself as a
better [Paxos](http://css.csail.mit.edu/6.824/2014/papers/paxos-simple.pdf),
but another way to look at Raft is that it solves a bigger problem
than Paxos. To build a real-world replicated service, the replicas
need to agree on an indefinite sequence of values (the client
commands), and they need ways to efficiently recover when servers
crash and restart or miss messages. People have built such systems
with Paxos as the starting point (e.g., Google's Chubby and Paxos
Made Live papers, and ZooKeeper/ZAB). There is also a protocol
called Viewstamped Replication; it's a good design, and similar to
Raft, but the paper about it is hard to understand.

These real-world protocols are complex, and (before Raft) there was not a good introductory paper describing how they work. The Raft paper, in contrast, is relatively easy to read and fairly detailed.

**Question**:
Suppose we have the scenario shown in the Raft paper's Figure 7: a cluster of seven
servers, with the log contents shown. The first server crashes (the one
at the top of the figure), and
cannot be contacted. A leader election ensues.
For each of the servers marked (a), (d), and (f), could that server
be elected?
If yes, which servers would vote for it? If no, what specific
Raft mechanism(s) would prevent it from being elected?

The lecture today covers effective approaches to debugging the 6.5840 labs. Submit a question about the testing and debugging process of your lab 1 solution: for example, something you struggled with, something you aren't confident about, or something you're curious about.

Could a received InstallSnapshot RPC cause the state machine to go backwards in time? That is, could step 8 in Figure 13 cause the state machine to be reset so that it reflects fewer executed operations? If yes, explain how this could happen. If no, explain why it can't happen.

Please read the paper's Appendices. In Spinnaker a leader to responds to a client request after the leader
and *one* follower have written a log record for the request on
persistent storage. Why is this sufficient to guarantee strong
consistency even after the leader or the one follower fail?

(This paper relies on Zookeeper, which we will read later.)

The lecture today is a Q&A session about Lab 3A/3B. Submit a question about the lab: for example, something you wondered about while doing the lab, something you didn't understand, a memorable bug, or just anything.

With a linearizable key/value storage system, could two clients who issue get() requests for the same key at the same time receive different values? Explain why not, or how it could occur.

One use of [Zookeeper](https://pdos.csail.mit.edu/papers/zookeeper.pdf) is as a fault-tolerant
lock service (see the section "Simple locks" on page 6). Why isn't possible
for two clients to acquire the same lock? In particular, how does
Zookeeper decide if a client has failed and it can give the client's locks to
other clients?

Item 4 in Section 2.3 says that, if a client read request arrives and the latest version is dirty, the node should ask the tail for the latest committed version. Suppose, instead, that the node replied with its most recent clean version (ignoring any dirty version and not sending a version query to the tail). This change would cause reads to reflect the most recent committed write that the node is aware of. Explain how this could lead to violations of linearizability -- or violations of the paper's goal of strong consistency.

Suppose Chain Replication replied to update requests from the head, as soon as the next chain server said it received the forwarded update, instead of responding from the tail. Explain how that could cause Chain Replication to produce results that are not linearizable.

The second paragraph of Section 4.1 says "The runtime state maintained by the database lets us use single segment reads rather than quorum reads..." What runtime state does the database need to maintain in order to avoid having to read from a quorum?

Russ Cox is one of the leads on the Go project. What do you like best about Go? Why? Would you want to change anything in the language? If so, what and why?

[6.033 Book](https://ocw.mit.edu/resources/res-6-004-principles-of-computer-system-design-an-introduction-spring-2009/online-textbook/).
Read just these parts of Chapter 9: 9.1.5, 9.1.6, 9.5.2, 9.5.3, 9.6.3. The
last two sections (on two-phase locking and distributed two-phase
commit) are the most important.
The Question: describe a situation where Two-Phase Locking yields higher performance than Simple Locking.

[Spanner](https://pdos.csail.mit.edu/papers/spanner.pdf)
Suppose a Spanner server's TT.now() returns correct
information, but the uncertainty is large. For example,
suppose the absolute time is 10:15:30, and TT.now()
returns the interval [10:15:20,10:15:40]. That interval
is correct in that it contains the absolute time, but the
error bound is 10 seconds.
See Section 3 for an explanation of TT.now().
What bad effect will a large error bound have on Spanner's operation?
Give a specific example.

At the end of Section 6.2, the
[Chardonnay](https://pdos.csail.mit.edu/papers/osdi23-eldeeb.pdf)
paper says that a snapshot read transaction can be made
linearizable by waiting for the epoch to advance by one.
By "linearizable" the paper means that the transaction
observes the results of all transactions that completed
before it started.
Why does waiting make the transaction linearizable?

[No compromises: distributed
transactions with consistency, availability, and performance](https://pdos.csail.mit.edu/papers/farm-2015.pdf):
Suppose there are two FaRM transactions that both increment the same
object. They start at the same time and see the same initial value for
the object. One transaction completely finishes committing (see
Section 4 and Figure 4). Then the second transaction starts to commit.
There are no failures. What is the evidence that FaRM will use to
realize that it must abort the second transaction? At what point in
the Section 4 / Figure 4 protocol will FaRM realize that it must
abort?

[Amazon DynamoDB: A scalable,
predictably performant, and fully managed NoSQL Database service](https://pdos.csail.mit.edu/papers/atc22-dynamodb.pdf)
To avoid interference, DynamoDB may throttle a customer's
application if it exceeds its read or write capacity, which can
cause the application to become unavailable. How does DynamoDB avoid
that a single hot partition of a database table can cause an
application to be unavailable?

[Distributed Transactions at
Scale in Amazon DynamoDB](https://pdos.csail.mit.edu/papers/atc23-idziorek.pdf).
Section 3.3 says, in the third bullet,
"The transaction's timestamp is greater than the
item's timestamp indicating when it was last written."
What's an example of an incorrect outcome that this check helps rule out?

[MDCC](https://pdos.csail.mit.edu/papers/mdcc.pdf)
Come back later for this year's question.

[Ownership: A Distributed Futures System for
Fine-Grained Tasks](https://pdos.csail.mit.edu/papers/ray.pdf).
If C() in figure 6(a) is as follows:

def C(x): z = D(X) return Get(z) # return value of future zSuppose the node than runs D fails before finishing, which node would initiates the re-execution of D()?

[Resilient Distributed Datasets: A
Fault-Tolerant Abstraction for In-Memory Cluster Computing](https://pdos.csail.mit.edu/papers/zaharia-spark.pdf)
What applications can Spark support well that MapReduce/Hadoop cannot support?

[Naiad: A Timely Dataflow System](https://pdos.csail.mit.edu/papers/naiad.pdf):
Consider the data-flow graph in Figure 3, and assume that the vertices are
instantiated as follows:

**A**is a distinct-by-key operator, which for inputs of`(key, value)`only emits the*first*`(key, value)`record with each distinct key.**B**is a multiply operator, which multiplies the value by two (i.e., for`(key, value)`, it emits`(key, value * 2)`.**C**is a conditional operator, which sends its output to**E**if the input`value`is greater than 10, and sends it to**F**otherwise.**D**is an aggregation operator that sums all values irrespective of key.

Now assume that we introduce two records in epoch *e* = 1 at the
**In** vertex: `(a, 2)` and `(b, 6)`; and one record in
*e* = 2: `(a, 5)`.

Write down the timestamp changes that the records experience as they flow
through the graph, e.g., `(a, 2): at A, t = (1, []); at B, t = ...`.
You may omit vertices that do not modify the timestamp.

Informally explain when `E.OnNotify((1, []))` will be called.
You do not need to step through the details of the pointstamp protocol.

[Parameter Server](https://pdos.csail.mit.edu/papers/parameter.pdf):
The parameter server model was developed for running machine-learning
algorithms like sparse logistic regression (§ 5.1).

What do you expect the bottleneck – that is, the most loaded –
resource (e.g., CPU, memory, network) to be at the **workers** and at
the **servers**?

What resource utilization would you likely observe if using Spark's logistic regression (see §3.2.1 in the Spark paper) instead of the parameter server for the experiment in §5.1?

[Frangipani: A Scalable
Distributed File System](https://pdos.csail.mit.edu/papers/thekkath-frangipani.pdf): Suppose a server modifies an i-node,
appends the modification to its log, then another server modifies the
same i-node, and then the first server crashes. The recovery system
will see the i-node modification in the crashed server's log, but
should not apply that log entry to the i-node, because that would
un-do the second server's change. How does Frangipani avoid or cope
with this situation?

[Memcache at Facebook](https://pdos.csail.mit.edu/papers/memcache-fb.pdf).
Section 3.3 implies that a client that writes data does not
delete the corresponding key from the Gutter servers, even
though the client does try to delete the key from the ordinary
Memcached servers (Figure 1). Explain why it would be a bad
idea for writing clients to delete keys from Gutter servers.

[COPS](https://pdos.csail.mit.edu/papers/cops.pdf). The last sentence in Section 4.3
says a client clears its context after a put, replacing the context
with just the put. The text observes "This put depends on all previous
key-version pairs and thus is nearer than them." Why does clearing the
context and replacing it with just the put make sense? You might think
that the client's subsequent puts would need to carry along the
dependency information about previous gets. What entity ultimately
uses the context information, and why does it not need the information
about gets before the last put?

Explain why it's important that all viewers of a Certificate Transparency log see the same content. What attacks would be possible if a malicious log server was able to cause some readers of its log to see one sequence of records, and other readers to see a different set of records? What mechanisms ensure that all viewers see the same log content?

Why is it important that Blockstack names be unique, human-readable, and decentralized? Why is providing all three properties hard?

[Managing Update Conflicts in Bayou](https://pdos.csail.mit.edu/papers/bayou-conflicts.ps)
Suppose we build a distributed filesystem using Bayou, and the
system has a copy operation. Initially, file A contains "foo"
and file B contains "bar". On one node, a user copies file A
to file B, overwriting the old contents of B. On another node, a
user copies file B to file A. After both operations are committed, we
want both files to contain "foo" or for both files to contain
"bar". Sketch a dependency check and merge procedure for the
copy operation that makes this work. How does Bayou ensure that
all the nodes agree about whether A and B contain "foo" or
"bar"?

For the design described in [Chord: a scalable
peer-to-peer lookup service for Internet applications](https://pdos.csail.mit.edu/papers/stoica-chord.pdf), if two Chord nodes
x and y are located nearby each other in the Internet (e.g., they are both in
the same datacenter), is the number of Chord hops small (say 1 or 2 instead of
log N) when x is looking up a key that is stored on node y?

[Dynamo](https://pdos.csail.mit.edu/papers/dynamo.pdf)
Suppose Dynamo server S1 is perfectly healthy with a working network
connection. By mistake, an administrator instructs server S2 to remove
S1 using the mechanisms described in 4.8.1 and 4.9. It takes a while
for the membership change to propagate from S2 to the rest of the
system (including S1), so for a while some clients and servers will
think that S1 is still part of the system. Will Dynamo operate
correctly in this situation? Why, or why not?

The [Zanzibar](https://pdos.csail.mit.edu/papers/zanzibar.pdf) paper says,
in the fourth paragraph of Section 4, that Zanzibar serves
a total of roughly 10 million client requests per second.
Section 4.4 says that the aclservers perform roughly 200 million
in-memory lookups per second. What could be the reason for
the order of magnitude difference?

The paper mentions that decryption increases latency for fetching a chunk in Section 5.1. Why encrypt chunks with convergent encryption in the first place?

Boki ensures that functions appear to execute exactly-once even though the function may be re-executed because of a machine failure. One challenge is that if the function updates an external database (e.g., updating a row in DynamoDB), this update must happen only once. How does Boki achieve this goal in Figure 6(a)?

[Secure Untrusted Data Repository (SUNDR)](https://pdos.csail.mit.edu/papers/li-sundr.pdf).
You only need to read through the end of 3.3.2.
In the simple straw-man, both fetch and modify operations are placed
in the log and signed. Suppose an alternate design that only signs and
logs modify operations. Does this allow a malicious server to break
fetch-modify consistency or fork consistency? Why or why not?

Suppose that we eliminated the pre-prepare phase from the Practical BFT protocol. Instead, the primary multicasts a PREPARE,v,n,m message to the replicas, and the replicas multicast COMMIT messages and reply to the client as before. What could go wrong with this protocol? Give a short example, e.g., ``The primary sends foo, replicas 1 and 2 reply with bar...''

[Bitcoin](https://pdos.csail.mit.edu/papers/bitcoin.pdf)
Try to buy something with Bitcoin. It may help to cooperate
with some 6.5840 class-mates, and it may help to start a
few days early.
If you decide to give up, that's OK. Briefly describe your experience.

[Ethereum Whitepaper](https://ethereum.org/en/whitepaper/).
Use an Ethereum decentralized application (dapp) and send a transaction to a smart contract.

- You will need an Ethereum wallet. For the purpose of this assignment,
[MetaMask](https://metamask.io/)is convenient and has integration with many dapps. - You can either acquire "real" (mainnet) Ethereum (e.g. by buying some using
[Coinbase](https://www.coinbase.com/buy-ethereum)) or acquire some free Sepolia testnet Ethereum using a "faucet" (you can use Google to find faucet websites). Note: not all dapps will support testnet Ethereum. - Find a dapp to interact with. You can find lists online, such as
[the dapp list](https://thedapplist.com/)and[DappRadar](https://dappradar.com/).

If you decide to give up, that's OK. Briefly describe your experience.

[IronFleet](https://pdos.csail.mit.edu/papers/ironfleet.pdf): Consider a Raft
implementation (written in Dafny) which does not implement the paper's
election restriction (i.e. followers do not check if the candidate's log is
up-to-date when voting). Where in Figure 3 could a developer get stuck while
applying the IronFleet methodology to this implementation?

[Experiences with a Distributed,
Scalable, Methodological File System: AnalogicFS](https://pdos.csail.mit.edu/papers/katabi-analogicfs.pdf). In many ways,
this experiences paper raises more questions than it answers. Please
answer one of the following questions, taking into consideration the
rich history of AnalogicFS and the spirit in which the paper was
written:

a) The analysis of A* search shown in Figure 1 claims to be an introspective visualization of the AnalogicFS methodology; however, not all decisions are depicted in the figure. In particular, if I <= P, what should be the next node explored such that all assumptions in Section 2 still hold? Show your work.

b) Despite the authors' claims in the introduction that AnalogicFS was developed to study SCSI disks (and their interaction with lambda calculus), the experimental setup detailed in Section 4.1 involves decommissioned Gameboys instead, which use cartridge-based, Flash-like memory. If the authors had used actual SCSI disks during the experiments, how exactly might have their results changed quantitatively?

c) AnalogicFS shows rather unstable multicast algorithm popularity (Figure 5), especially compared with some of the previous systems we've read about in 6.5840. Give an example of another system that would have a more steady measurement of popularity pages, especially in the range of 0.1-0.4 decibels of bandwidth.

d) For his 6.5840 project, Ben Bitdiddle chose to build a variant of Lab 5 that faithfully emulates the constant expected seek time across LISP machines, as AnalogicFS does. Upon implementation, however, he immediately ran into the need to cap the value size to 400 nm, rather than 676 nm. Explain what assumptions made for the AnalogicFS implementation do not hold true for Lab 5, and why that changes the maximum value size.

Questions or comments regarding 6.5840? Send e-mail to [ 6824-staff@lists.csail.mit.edu](mailto:6824-staff@lists.csail.mit.edu).

** Top** //
