Title: l13.pdf
Mapped Topic: Network systems course notes
Source URL: https://www.scs.stanford.edu/10au-cs144/notes/l13.pdf
Source Type: university_course_notes
Trust Score: 95
Fetched At: 2026-04-17T06:57:19+00:00
Mapped From CSE.md Section: Part 1 / Part 2.B

# Content

Lecture 13: Coding, Error Detection and
Correction

Errors and Losses
• Physical layers use encoding to protect link layer
from chip errors
• All or nothing: if chip errors exceed layer 1
robustness, you lose the whole packet (bad CRC)
• We can use these techniques at higher layers as
well: erasure coding
- Encoding data of length L as k symbols: any n of the k
symbols can regenerate the original data ( n ≥ L ).

Cyclic Redundancy Check (CRC), revisited
• Distill n bits of data into a c bit CRC, c<<n
• Can’t detect all errors ( 2
− c
chance another packet’s
CRC matches)
• CRCs are designed to detect certain forms of errors
more than others
• Stronger than checksums; detect
- A message with any 1 or 2 bits in error
- A message with any odd number of errors
- A message with an error burst as wide as the CRC

Message Authenticaion Codes
• When sending packets securely (conﬁdentially),
sometimes you use a Message Authentication
Code (MAC) instead of a CRC
• Kind of like a CRC, but seeded with a secret
• MAC needs different properties to be strong
against attackers
- If any bit in the message changes, each bit in the MAC
needs to have an equal probability of being 0 or 1
- Starting with packet P , can’t append data and generate
new MAC
- Can ﬂip a bit and get the same MAC value

Cyclic Redundancy Check, continued
• Can be computed iteratively (e.g., as a packet is
spooled out)
• Mathematical basis
- CRC of length n computed as an n th degree polynomial
- CRC of length n is remainder after dividing message by a
number k> 2
n
- k = 25 , k = 11001 , x
4
+ x
3
+ x
0
• To detect burst errors of length b , n>b

Fields
• A set of numbers of which you can add, subtract,
multiply, and divide
• A ﬁeld can be ﬁnite (Galois Field)
• E.g., Galois Field GF ( p ) ﬁeld of integers modulo p ,
p is prime
• In GF (7) , 6 + 3 = 2

Reed-Solomon
• Standard erasure coding technique: used in CDs
• Core idea: any k distinct data points deﬁne a
unique polynomial of degree k − 1
• Data to transmit deﬁnes the polynomial P
• Compute coded data C = P ( x ) for x 0 ,x 1 ,x n
• Transmit C
• A receiver that gets k different x n values can
reconstitute original polynomial (and data)

Power of Erasure Coding
• Make data k − 1 term polynomial
• Compute n data points, where n>k
• Any k data points can successfully regenerate data
• Can tolerate n − k losses, or
n − k
2
errors
• Known errors/losses are called erasures: erasure
coding

Code Word Sizes
• Large polynomials lead to large values: 63 · 19
10
!
• Reed-Solomon works on ﬁelds
• GF(256), 63 · 19
10
= 106
• Reed-Solomon uses GF(256);
• Sends 223 data symbols, 32 symbols are parity
values (223,255)
• 8 bits can have very efﬁcient implementations

Error Burstiness
• Reed-Solomon divides data into code symbols
(e.g., 8 bits)
• Any one bit error invalidates that symbol
• Robust to bursts of errors, weaker against random
errors
• Big bursts can overwhelm the code: CDs use
Cross-Interleaved Reed-Solomon Coding (CIRC)
to spread errors across symbol blocks

Reed-Solomon
• Useful for making media more resilient: operates
on small datum
• Increasing the coding factor k increases
robustness: can be made robust to arbitrary losses
• Is there some way to do something similar on large
data (e.g., packets?)

Erasure Codes, Revisited
• Data of length k
• Erasure codes can regenerate data from any
k (1 + γ ) code symbols
• Do not necessarily handle errors
• Perfect world, γ = 0 (not possible in practice)
• Also want decoding to be fast/simple

Problem Statement
• Have a large piece of data
• Want to deliver it to many client nodes
• Do not want to maintain per-client state
• Goal: send packets, any k packets can reconsitute
data with very high probability
• Example: television over IP

Why Not Reed-Solomon
• We’re operating on a very large piece of data
• Can deal with larger chunks than Reed-Solomon
• Allows us to do something simpler?

LT Codes
• Data of length N
• Code words of length l , any l will do!
• Break data into k = ⌈
D
L
⌉ chunks C
• Each transmitted packet C i is an XOR of some
number of random chunks
• Symbol generation is O (ln( k/δ )) on average
• Requires k + O (
√
k ln
2
( k/δ )) symbols to decode
with probability 1 − δ

Power of XOR
• Data A, B, C, D
• Have x 0 = A,x 1 = A ⊕ B,x 2 = A ⊕ C,x 3 = C ⊕ D
• A = x 0
• B = A ⊕ x 1
• C = A ⊕ x 2
• D = C ⊕ x 3

XOR, Visually

How to XOR?
• How LT codes XOR the data into code words is
critical
• d ( C i ) is the degree of codeword i : how many data
items are XORed in it
• Example bad distributions
- ∀ C i ,d ( C i ) = 1 : sending data in the clear
- ∀ C i ,d ( C i ) = k − 1 : each codeword is the XOR of all but one
data symbol
- Both have k unique code words, and require receiving all k

Codeword Degree

LT Decoding Algorithm
• We receive n codewords
• Initially, all input symbols are uncovered
• Each codeword with d = 1 covers the input symbol
• Ripple: set of covered input symbols that have not
been processed
• For each symbol in the ripple
- Scan across the codewords and remove it from those that
have it (via XOR), reducing degree by 1
- If codeword has degree 1, cover its input symbol

LT Decoding
• Decoding stops when the ripple is size 0
- If all input symbols are covered, success
- If any input sybmols are uncovered, failure
• How big should the ripple be?
- Small, so there is low redundancy in coverage
- Never zero, because that halts decoding
• Control ripple size through degree distribution ρ

2-minute break

LT Encoding
• Two goals
- Minimize number of needed encoding symbols (bps)
- Minimize average degree of encoding symbols (CPU cycles)
• Step through three examples:
- All-at-once: ρ (1) = 1
- Ideal: ρ (1) = 1 /k,ρ ( i ) = 1 /i ( i − 1)
- Robust: more on this later

All-at-once
• How many encoded symbols does it take?
• Bins and balls: how many balls must be thrown to
ensure that there is one in each of k bins?
• O ( k · ln( k/δ )) for probability 1 − δ
• Requires ln( k/δ ) factor (on average ln( k ) )
• k = 1000 ,δ = 0 . 01% , ln(10
7
) = 16

Ideal distribution
• ρ (1) = 1 /k , ∀ i,i = 2 ,...,k,ρ ( i ) = 1 /i ( i − 1)
• Expected behavior is perfect: one input has a d of
1, each cover releases another symbol
• Requires k symbols, sum of degrees is k · ln( k )
• Same sum of degrees as all-at-once, but only k
symbols

The World Is Not Ideal
• “However, this heuristic analysis makes the
completely unrealistic assumption that the
expected behavior is the actual behavior, and this
is far from the truth. In fact, the Ideal Soliton
distribution works very poorly in practice because
he expected size of the ripple is one, and even the
smallest variance causes the ripple to vanish and
thus the overall process fails to cover and process
all input symbols.” (Luby)

Robust Distribution
• Size of ripple behaves like a random walk
• Goal: make median point of random walk large
enough to survive variations ( ln ( k/δ )
√
k )
• Deﬁne a constant R , R = c · ln( k/δ )
√
k
τ ( i ) =



R/ik i = 1 ,...,k/R − 1
R ln( R/δ ) /k i = k/R
0 i = l/R + 1 ,...,k
• Add τ to ρ of Ideal, normalize

Improvements of Robust Distribution
• τ skews Ideal towards smaller degrees
• Requires k + O (
√
k · ln
2
( kδ )) (additive factor!)
• k = 1000 ,δ = 0 . 01% , requires an extra 88 symbols,
8% overhead.
• Average degree is still ln( k/δ )

Implications
• Example: server wants to deliver 1MB image (1000
1kB packets)
• Server generates packets from robust distribution
• No matter the properties of the lossy channel
(burstiness, periodicity, etc.), there is a 99.99%
chance that a client will be able to regenerate the
image after 1088 packets
• Uses only ln( k/δ ) (e.g., 16) XOR operations per
packet
• Hence the name, “Fountain Code”

MORE
• Chachulski et al., SIGCOMM 2007.
• “MAC-independent Opportunistic Routing &
Encoding”
• Uses network coding in wireless networks to
improve throughput
• Works with unicast ﬂows as well as multicast!
• Sachin Katti, starting in EE/CS in January,
co-authored

Motivation
Unicast
Figure 1—Unicast Example. The source sends 2 packets. The destination
overhears p1, while R receives both. R needs to forward just one packet but,
without node-coordination, it may forward p1, which is already known to
the destination. With network coding, however, R does not need to know
which packet the destination misses. R just sends the sum of the 2 packets
p1 + p2. This coded packet allows the destination to retrieve the pa cket it
misses independently of its identity. Once the destination receives the whole
transfer (p1 and p2), it acks the transfer causing R to stop transmitting.
routing and MAC layers. MORE is MAC-independent, and thus
can enjoy the basic features available to today’s MAC. Speciﬁ-
cally, it achieves better unicast throughput by exploiting the spa-
tial reuse available with 802.11. Further, the clean separation be-
tween the layers makes MORE easily extensible to multicast traf-
ﬁc.
• On the other hand, MORE presents a low-complexity distributed
and 802.11-compatible algorithm for intra-ﬂow network coding
over wireless unicast ﬂows. Prior work requires solving a con-
vex optimization with constraints that grow exponentially with
the maximum number of nodes reached by a broadcast [27, 28].
MORE also presents the ﬁrst implementation of wireless intra-
ﬂow network coding, demonstrating the practical beneﬁts of mix-
ing packets within a wireless ﬂow.1
2. M OTIVATING EXAMPLES
MORE’s design builds on the theory of network coding [2, 26,
15]. In this section, we use two toy examples to explain the intuition
underlying our approach and illustrate the synergy between oppor-
tunistic routing and network coding.
The Unicast Case: Consider the scenario in Fig. 1. Traditional rout-
ing predetermines the path before transmission. It sends trafﬁc along
the path “src→ R→ dest”, which has the highest delivery probability.
However, wireless is a broadcast medium. When a node transmits,
there is always a chance that a node closer than the chosen next-
hop to the destination overhears the packet. For example, assume
the source sends 2 packets,p1 and p2. The nexthop, R, receives both,
and the destination happens to overhear p1. It would be a waste to
have node R forward p1 again to the destination. This observation
has been noted in [7] and used to develop ExOR, an opportunistic
routing protocol for mesh wireless networks.
ExOR, however, requires node coordination, which is more difﬁ-
cult in larger networks. Consider again the example in the previous
paragraph. R should forward only packet p2 because the ﬁrst packet
has already been received by the destination; but, without consulting
with the destination,R has no way of knowing which packet to trans-
mit. The problem becomes harder in larger networks, where many
nodes hear a transmitted packet. Opportunistic routing allows these
nodes to participate in forwarding the heard packets. Without co-
ordination, however, multiple nodes may unnecessarily forward the
same packets, creating spurious transmissions. To deal with this is-
sue, ExOR imposes a special scheduler on top of 802.11. The sched-
uler goes in rounds and reserves the medium for a single forwarder
1In contrast, COPE [23] is the ﬁrst implementation that demon-
strates practical beneﬁts for inter-ﬂow wireless network coding.
Figure 2—Multicast Example. Instead of retransmitting all four packets,
the source can transmit two linear combinations, e.g., p1 + p2 + p3 + p4 and
p1 + 2p2 + 3p3 + 4p4. These two coded packets allow all three destinations
to retrieve the four original packets, saving the source 2 transmissions.
at any one time. The rest of the nodes listen to learn the packets over-
heard by each node. Due to this strict schedule, nodes farther away
from the destination (which could potentially have transmitted at the
same time as nodes close to the destination due to spatial reuse),
cannot, since they have to wait for the nodes close to the destina-
tion to ﬁnish transmitting. Hence the scheduler has the side effect of
preventing a ﬂow from exploiting spatial reuse.
Network coding offers an elegant solution to the above problem.
In our example, the destination has overheard one of the transmit-
ted packets, p1, but node R is unaware of this fortunate reception.
With network coding, nodeR naturally forwards linear combinations
of the received packets. For example, R can send the sum p1 + p2.
The destination retrieves the packet p2 it misses by subtracting from
the sum and acks the whole transfer. Thus, R need not know which
packet the destination has overheard.
Indeed, the above works ifR sends any random linear combination
of the two packets instead of the sum. Thus, one can generalize the
above approach. The source broadcasts its packets. Routers create
random linear combinations of the packets they hear (i.e., c1p1 +
. . . + cnpn, where ci is a random coefﬁcient). The destination sends
an ack along the reverse path once it receives the whole transfer. This
approach does not require node coordination and preserves spatial
reuse.
The Multicast Case: Our second example illustrates the synergy
between network coding and multicast. In Fig. 2, the source multi-
casts 4 packets to three destinations. Wireless receptions at different
nodes are known to be highly independent [32, 30]. Assume that
each destination receives the packets indicated in the ﬁgure–i.e., the
ﬁrst destination receives p1 and p2, the second destination receives
p2 and p3, and the last destination receives p3 and p4. Note that each
of the four packets is lost by some destination.
Without coding, the sender has to retransmit the union of all
lost packets, i.e., the sender needs to retransmit all four packets.
In contrast, with network coding, it is sufﬁcient to transmit 2 ran-
domly coded packets. For example, the sender may send p′
1 =
p1 + p2 + p3 + p4 and p′
2 = p1 + 2p2 + 3p3 + 4p4. Despite the fact
that they lost different packets, all three destinations can retrieve the
four original packets using these two coded packets. For example,
the ﬁrst destination, which has received p′
1, p′
2 and p1, p2, retrieves
all four original packets by inverting the matrix of coefﬁcients, and
multiplying it with the packets it received, as follows:
0
B
B
@
p1
p2
p3
p4
1
C
C
A =
0
B
B
@
1 1 1 1
1 2 3 4
1 0 0 0
0 1 0 0
1
C
C
A
− 1 0
B
B
@
p′
1
p′
2
p1
p2
1
C
C
A .
Thus, in this simple example, network coding has reduced the
needed retransmissions from 4 packets to 2, improving the overall
throughput.
Multicast
Figure 1—Unicast Example. The source sends 2 packets. The destination
overhears p1, while R receives both. R needs to forward just one packet but,
without node-coordination, it may forward p1, which is already known to
the destination. With network coding, however, R does not need to know
which packet the destination misses. R just sends the sum of the 2 packets
p1 + p2. This coded packet allows the destination to retrieve the pa cket it
misses independently of its identity. Once the destination receives the whole
transfer (p1 and p2), it acks the transfer causing R to stop transmitting.
routing and MAC layers. MORE is MAC-independent, and thus
can enjoy the basic features available to today’s MAC. Speciﬁ-
cally, it achieves better unicast throughput by exploiting the spa-
tial reuse available with 802.11. Further, the clean separation be-
tween the layers makes MORE easily extensible to multicast traf-
ﬁc.
• On the other hand, MORE presents a low-complexity distributed
and 802.11-compatible algorithm for intra-ﬂow network coding
over wireless unicast ﬂows. Prior work requires solving a con-
vex optimization with constraints that grow exponentially with
the maximum number of nodes reached by a broadcast [27, 28].
MORE also presents the ﬁrst implementation of wireless intra-
ﬂow network coding, demonstrating the practical beneﬁts of mix-
ing packets within a wireless ﬂow.1
2. M OTIVATING EXAMPLES
MORE’s design builds on the theory of network coding [2, 26,
15]. In this section, we use two toy examples to explain the intuition
underlying our approach and illustrate the synergy between oppor-
tunistic routing and network coding.
The Unicast Case: Consider the scenario in Fig. 1. Traditional rout-
ing predetermines the path before transmission. It sends trafﬁc along
the path “src→ R→ dest”, which has the highest delivery probability.
However, wireless is a broadcast medium. When a node transmits,
there is always a chance that a node closer than the chosen next-
hop to the destination overhears the packet. For example, assume
the source sends 2 packets,p1 and p2. The nexthop, R, receives both,
and the destination happens to overhear p1. It would be a waste to
have node R forward p1 again to the destination. This observation
has been noted in [7] and used to develop ExOR, an opportunistic
routing protocol for mesh wireless networks.
ExOR, however, requires node coordination, which is more difﬁ-
cult in larger networks. Consider again the example in the previous
paragraph. R should forward only packet p2 because the ﬁrst packet
has already been received by the destination; but, without consulting
with the destination,R has no way of knowing which packet to trans-
mit. The problem becomes harder in larger networks, where many
nodes hear a transmitted packet. Opportunistic routing allows these
nodes to participate in forwarding the heard packets. Without co-
ordination, however, multiple nodes may unnecessarily forward the
same packets, creating spurious transmissions. To deal with this is-
sue, ExOR imposes a special scheduler on top of 802.11. The sched-
uler goes in rounds and reserves the medium for a single forwarder
1In contrast, COPE [23] is the ﬁrst implementation that demon-
strates practical beneﬁts for inter-ﬂow wireless network coding.
Figure 2—Multicast Example. Instead of retransmitting all four packets,
the source can transmit two linear combinations, e.g., p1 + p2 + p3 + p4 and
p1 + 2p2 + 3p3 + 4p4. These two coded packets allow all three destinations
to retrieve the four original packets, saving the source 2 transmissions.
at any one time. The rest of the nodes listen to learn the packets over-
heard by each node. Due to this strict schedule, nodes farther away
from the destination (which could potentially have transmitted at the
same time as nodes close to the destination due to spatial reuse),
cannot, since they have to wait for the nodes close to the destina-
tion to ﬁnish transmitting. Hence the scheduler has the side effect of
preventing a ﬂow from exploiting spatial reuse.
Network coding offers an elegant solution to the above problem.
In our example, the destination has overheard one of the transmit-
ted packets, p1, but node R is unaware of this fortunate reception.
With network coding, nodeR naturally forwards linear combinations
of the received packets. For example, R can send the sum p1 + p2.
The destination retrieves the packet p2 it misses by subtracting from
the sum and acks the whole transfer. Thus, R need not know which
packet the destination has overheard.
Indeed, the above works ifR sends any random linear combination
of the two packets instead of the sum. Thus, one can generalize the
above approach. The source broadcasts its packets. Routers create
random linear combinations of the packets they hear (i.e., c1p1 +
. . . + cnpn, where ci is a random coefﬁcient). The destination sends
an ack along the reverse path once it receives the whole transfer. This
approach does not require node coordination and preserves spatial
reuse.
The Multicast Case: Our second example illustrates the synergy
between network coding and multicast. In Fig. 2, the source multi-
casts 4 packets to three destinations. Wireless receptions at different
nodes are known to be highly independent [32, 30]. Assume that
each destination receives the packets indicated in the ﬁgure–i.e., the
ﬁrst destination receives p1 and p2, the second destination receives
p2 and p3, and the last destination receives p3 and p4. Note that each
of the four packets is lost by some destination.
Without coding, the sender has to retransmit the union of all
lost packets, i.e., the sender needs to retransmit all four packets.
In contrast, with network coding, it is sufﬁcient to transmit 2 ran-
domly coded packets. For example, the sender may send p′
1 =
p1 + p2 + p3 + p4 and p′
2 = p1 + 2p2 + 3p3 + 4p4. Despite the fact
that they lost different packets, all three destinations can retrieve the
four original packets using these two coded packets. For example,
the ﬁrst destination, which has received p′
1, p′
2 and p1, p2, retrieves
all four original packets by inverting the matrix of coefﬁcients, and
multiplying it with the packets it received, as follows:
0
B
B
@
p1
p2
p3
p4
1
C
C
A =
0
B
B
@
1 1 1 1
1 2 3 4
1 0 0 0
0 1 0 0
1
C
C
A
− 1 0
B
B
@
p′
1
p′
2
p1
p2
1
C
C
A .
Thus, in this simple example, network coding has reduced the
needed retransmissions from 4 packets to 2, improving the overall
throughput.

MORE at Layer 2.5

MORE at Layer 2.5

MORE Summary
• A coded packet is a linear combination of native
packets
• MORE adds a header that contains the linear
coefﬁcients
• MORE uses opportunistic reception: nodes
broadcast coded packets to some number of next
hops, more than one of which can forward the
packet
• Source collects native packets into a batch, starts
sending linear combinations of those packets,
stops when it receives an end-to-end ACK.

Opportunistic Reception
• MORE maintains ETX-based route estimates
• MORE picks n forwarders which are closer to the
destination than it, ordered according to their
proximity ( n closest)

Forwarding Packets
• Some received coded packets are innovative: they
are linearly independent of prior packets
(bounded by batch size K )
• Forwarders discard packets that are not innovative
• Whenever a forwarder receives a packet, it gets a
transmit credit
• Sending a packet costs a credit
• ETX ordering prevents loops and credit explosion

Encoding and Decoding Packets
• Source makes each encoded packet a random
linear combination of native packets
• Forwarders send random linear combinations of
encoded packets (which are still linear
combinations)
• K linearly independent combinations allow the
destination to decode packet through simple
matrix inversion.

When To Stop?
• When destination determines it can decode, it
immediately sends an end-to-end ACK (don’t even
wait for decoding)
• Every node that hears the ACK stops
• When the source stops, forwarders stop getting
transmit credits
• ACK packets are put on fast path: take precedence
over all data packets

Improvement
Figure 5—One Floor of our Testbed. Nodes’ location on one ﬂoor of our
3-ﬂoor testbed.
antenna. They transmit at a power level of 18 dBm, and operate in
the 802.11 ad hoc mode, with RTS/CTS disabled.
(c) Software: Nodes in the testbed run Linux, the Click toolkit [25]
and the Roofnet software package [1]. Our implementation runs as
a user space daemon on Linux. It sends and receives raw 802.11
frames from the wireless device using a libpcap-like interface.
8.2 Compared Protocols
We compare the following three protocols.
• MORE as explained in §6.
• ExOR [7], the current opportunistic routing protocol. Our ExOR
code is provided by its authors.
• Srcr [6] which is a state-of-the-art best path routing protocol for
wireless mesh networks. It uses Dijkstra’s shortest path algorithm
where link weights are assigned based on the ETX metric [11].
8.3 Setup
In each experiment, we run Srcr, MORE, and ExOR in sequence
between the same source destination pairs. Each run transfers a 5
MByte ﬁle. We leverage the ETX implementation provided with the
Roofnet software to measure link delivery probabilities. Before run-
ning an experiment, we run the ETX measurement module for 10
minutes to compute pair-wise delivery probabilities and the corre-
sponding ETX metric. These measurements are then fed to all three
protocols, Srcr, MORE, and ExOR, and used for route selection.
Unless stated differently, the batch size for both MORE and ExOR
is set to K = 32 packets. The packet size for all three protocols is
1500B. The queue size at Srcr routers is 50 packets. In contrast,
MORE and ExOR do not use queues; they buffer active batches.
Most experiments are performed over 802.11b with a bit-rate of
5.5Mb/s. In §8.7, we allow traditional routing (i.e., Srcr) to exploit
the autorate feature in the MadWiﬁ driver, which uses the Onoe
bit-rate selection algorithm [5]. Current autorate control optimizes
the bit-rate for the nexthop, making it unsuitable for opportunistic
routing, which broadcasts every transmission to many potential nex-
thops. The problem of autorate control for opportunistic routing is
still open. Thus in our experiments, we compare Srcr with autorate
to opportunistic routing (MORE and ExOR) with a ﬁxed bit-rate of
11 Mb/s.
8.4 Throughput
We would like to examine whether MORE can effectively exploit
opportunistic receptions to improve the throughput and compare it
with Srcr and ExOR.
0
0.1
0.2
0.3
0.4
0.5
0.6
0.7
0.8
0.9
1
0 50 100 150 200
Cumulative Fraction of Flows
Throughput [pkt/s]
Srcr
ExOR
MORE
Figure 6 —Unicast Throughput . Figure shows the CDF of the uni-
cast throughput achieved with MORE, ExOR, and Srcr. MORE’s me dian
throughput is 22% higher than ExOR. In comparison to Srcr, MORE achieves
a median throughput gain of 95%, while some source-destination pairs show
as much as 10-12x.
(a) How Do the Three Protocols Compare? Does MORE improve
over ExOR? How do these two opportunistic routing protocols com-
pare with traditional best path routing? To answer these questions,
we use these protocols to transfer a 5 MByte ﬁle between various
nodes in our testbed. We repeat the same experiment for MORE,
ExOR, and Srcr as explained in §8.3.
Our results show that MORE signiﬁcantly improves the unicast
throughput. In particular, Fig. 6 plots the CDF of the through-
put taken over 200 randomly selected source-destination pairs in
our testbed. The ﬁgure shows that both MORE and ExOR signif-
icantly outperform Srcr. Interestingly, however, MORE’s through-
put is higher than ExOR’s. In the median case, MORE has a 22%
throughput gain over ExOR. Its throughput gain over Srcr is 95%,
but some challenged ﬂows achieve 10-12 x higher throughput with
MORE than traditional routing.
Further, MORE and opportunistic routing ease the problem of
dead spots. Fig. 6 shows that over 90% of MORE ﬂows have a
throughput larger than 51 packets a second. ExOR’s 10 th percentile
is at 35 packets a second. Srcr on the other hand suffers from dead
spots with many ﬂows experiencing very low throughput. Speciﬁ-
cally, the 10th percentile of Srcr’s throughput is at 12 packets a sec-
ond.
(b) When Does Opportunistic Routing Win? We try to identify
the scenarios in which protocols like MORE and ExOR are partic-
ularly useful, i.e., when should one expect opportunistic routing to
bring a large throughput gain? Fig. 7a shows the scatter plot for the
throughputs achieved under Srcr and MORE for the same source-
destination pair. Fig. 7b gives an analogous plot for ExOR. Points
on the 45-degree line have the same throughput in the two compared
schemes.
These ﬁgures reveal that opportunistic routing (MORE and
ExOR) greatly improves performance for challenged ﬂows, i.e.,
ﬂows that usually have low throughput. Flows that achieve good
throughput under Srcr do not improve further. This is because when
links on the best path have very good quality, there is little ben-
eﬁt from exploiting opportunistic receptions. In contrast, a source-
destination pair that obtains low throughput under Srcr does not have
any good quality path. Usually, however, many low-quality paths ex-
ist between the source and the destination. By using the combined
capacity of all these low-quality paths, MORE and ExOR manage to
boost the throughput of such ﬂows.
(c) Why Does MORE Have Higher Throughput than ExOR?
Our experiments show that spatial reuse is a main contributor to
MORE’s gain over ExOR. ExOR prevents multiple forwarders from
accessing the medium simultaneously [7], and thus does not exploit

Long Routes
1
10
100
1 10 100
MORE Throughput [pkt/s]
Srcr Throughput [pkt/s]
(a) MORE vs. Srcr
1
10
100
1 10 100
ExOR Throughput [pkt/s]
Srcr Throughput [pkt/s]
(b) ExOR vs. Srcr
Figure 7—Scatter Plot of Unicast Throughput.Each point represents the
throughput of a particular source destination pair. Pointsabove the 45-degree
line indicate improvement with opportunistic routing. The ﬁg ure shows that
opportunistic routing is particularly beneﬁcial to challenged ﬂows.
0
0.2
0.4
0.6
0.8
1
10 20 30 40 50 60 70
Cumulative Fraction of Flows
Throughput [pkt/s]
Srcr
ExOR
MORE
Figure 8—Spatial Reuse. The ﬁgure shows CDFs of unicast throughput
achieved by MORE, ExOR, and Srcr for ﬂows that traverse 4 hops , where
the last hop can transmit concurrently with the ﬁrst hop. MORE ’s median
throughput is 45% higher than ExOR.
spatial reuse. To examine this issue closely, we focus on a few ﬂows
that we know can beneﬁt from spatial reuse. Each ﬂow has a best
path of 4 hops, where the last hop can send concurrently with the
ﬁrst hop without collision. Fig. 8 plots the CDF of throughput of the
three protocols for this environment. Focusing on paths with spatial
reuse ampliﬁes the gain MORE has over ExOR. The ﬁgure shows
that for 4-hop ﬂows with spatial reuse, MORE achieves a 45% higher
median throughput than ExOR.
It is important to note that spatial reuse may occur even for shorter
paths. The capture effect allows multiple transmissions to be cor-
rectly received even when the nodes are within the radio range of
both senders [32]. In particular, less than 7% of the ﬂows in Fig. 6
have a best path of 4 hops or longer. Still MORE does better than
Figure 9—Multicast Topology. A simple topology used in the multicast
experiments in Fig. 10.
0
50
100
150
200
250
2 3 4
Throughput Per Destination [pkt/s]
Number of Destinations
Srcr
ExOR
MORE
Figure 10—Multicast Throughput as a Function of the Number of Des-
tinations for the Topology in Fig. 9. The ﬁgure shows the per-destination
multicast throughput of MORE, ExOR, and Srcr. The thick bars s how the
average per-destination throughput taken over 40 runs with different nodes.
The lines show the standard deviation.
ExOR. This is mainly because of capture. The capture effect, how-
ever, is hard to quantify or measure. Thus, we have focused on longer
paths to show the impact of spatial reuse.
8.5 Multicast
We want to compare the performance of multicast trafﬁc under
MORE, ExOR, and Srcr. In §7, we described how multicast works
under MORE. In contrast, ExOR [7] and Srcr [6] do not have mul-
ticast extensions. Thus, we need to deﬁne how these protocols deal
with multicast. For Srcr we adopt the same approach as wired mul-
ticast. Speciﬁcally, we ﬁnd the shortest path from the source to each
destination, using ETX as the metric. These paths create a tree rooted
at the source. Srcr’s multicast trafﬁc is sent along the branches of this
tree. In contrast, with ExOR, we want multicast trafﬁc to exploit op-
portunistic receptions. We ﬁnd the ExOR forwarders for each des-
tination. The per-destination forwarders use the ExOR protocol to
access the medium and coordinate their transmissions. In contrast
to unicast ExOR, if the forwarders toward destination X opportunis-
tically hear a packet by a forwarder in the forwarder list of desti-
nation Y, they exploit that opportunistic reception. Said differently,
we allow opportunistic receptions across the forwarders of various
destinations.
Our results show that MORE’s multicast throughput is signiﬁ-
cantly higher than both ExOR and Srcr. In particular, we experiment
with the simple topology in Fig. 9, where the source multicasts a ﬁle
to a varying number of destinations. Fig. 10 shows the average mul-
ticast throughput as a function of the number of destinations. The
average is computed over 40 different instantiations of the topology
in Fig 9, using nodes in our testbed. As expected, the per-destination
average throughput decreases with increased number of destinations.
Interestingly, however, the ﬁgure shows that MORE’s throughput
gain increases with increased number of destinations. MORE has
35-200% throughput gain over ExOR and 100-300% gain over Srcr.
MORE’s multicast throughput gain is higher than its unicast gain.
This is because network coding ﬁts naturally with multicast. Recall
from the example in §2 that without network coding, a transmitter

Batch Size
0
0.2
0.4
0.6
0.8
1
0 50 100 150 200
Cumulative Fraction of Flows
Throughput [pkt/s]
MORE, K=8
MORE, K=16
MORE, K=32
MORE, K=64
MORE, K=128
(a) MORE
0
0.2
0.4
0.6
0.8
1
0 50 100 150 200
Cumulative Fraction of Flows
Throughput [pkt/s]
ExOR, K=8
ExOR, K=16
ExOR, K=32
ExOR, K=64
ExOR, K=128
(b) ExOR
Figure 14 —Impact of Batch Size. The ﬁgure shows the CDF of the
throughput taken over 40 random node pairs. It shows that MOR E is less
sensitive to the batch size than ExOR.
confusing collision drops from error drops and unnecessarily reduc-
ing the bit-rate.
A close examination of the traces indicates that the auto-rate algo-
rithm often picks the lowest bit-rate in an attempt to reduce packet
loss; however, the improvement in quality of the relatively good
links is limited, and a large fraction of the losses is due to inter-
ference thus cannot be avoided by reducing the bit-rate. This lim-
ited beneﬁt is greatly outweighed by the sacriﬁce in bandwidth ef-
ﬁciency. In our experiments, the average success rate of all trans-
missions improves only slightly with autorate from 66% to 68%. At
the same time, on average 23% of all transmissions using autorate
are done at the lowest bit-rate, which takes roughly 10 times longer
than the highest bit-rate. These transmissions form a throughput bot-
tleneck and consume almost 70% of the shared medium time. As
shown in Fig. 13, this problem affects about 80% of all ﬂows tested.
8.8 Batch Size
We explore the performance of MORE and ExOR for various
batch sizes. Fig. 14 plots the throughput for batch sizes of 8, 16, 32,
64, and 128. It shows that ExOR’s performance with small batches
of 8 packets is signiﬁcantly worse than large batches. In contrast,
MORE is highly insensitive to different batch sizes.
In both ExOR and MORE, the overhead increases with reduced
batch size. ExOR nodes exchange control packets whenever they
transmit a batch. Increasing the batch size allows ExOR to amortize
the control trafﬁc and reduces the chance of spurious transmissions.
MORE may make a few spurious transmissions between the time
the destination decodes a batch and when the source and forwarders
stop transmitting packets from that batch. A bigger batch size allows
MORE to amortize the cost of these spurious transmissions over a
larger number of packets, increasing the overall throughput.
Insensitivity to batch sizes allows MORE to vary the batch size to
accommodate different transfer sizes. We expect that for any transfer
size larger than 7-10 packets (i.e., a batch larger than 7-10 packets),
MORE will show signiﬁcant advantages. Shorter transfers can be
Operation Avg. Time [µs] Std. Dev. [µs]
Independence check 10 5
Coding at the source 270 15
Decoding 260 150
Table 2—Average computational cost of packet operations in MORE.
The numbers for K = 32 and 1500B packets are measured on a low-end
Celeron machine clocked at 800MHz with 128KiB cache. Note that the cod-
ing cost is highest at the source because it has to code allK packets together.
The coding cost at a forwarder depends on the number of innovative packets
it has received, and is always bounded by the coding cost at the source.
sent using traditional routing. Note that MORE benignly co-exists
with traditional routing, which it uses to deliver its ACKs.
8.9 MORE’s Overhead
Finally, we would like to estimate MORE’s overhead and its suit-
ability for deployment in mesh networks like Roofnet [1] and com-
munity wireless networks [34, 3].
(a) Coding Overhead: In MORE, the cost of coding/decoding pack-
ets is incurred mainly when the packet has to be multiplied by a ran-
dom number (in a ﬁnite ﬁeld of size 28). To optimize this operation,
our implementation reduces the cost by using a 64KiB lookup-table
indexed by pairs of 8 bits. The lookup table caches results of all
possible multiplications, so multiplying any byte of a packet with a
random number is simply a fast lookup.
Table 2 provides micro benchmarks for coding and decoding in
MORE. The measurements are taken on a low-end Celeron 800MHz
machine. The benchmarks show that coding and decoding have
roughly equal cost. They require on average K ﬁnite-ﬁeld multipli-
cations per byte, where K is the batch size. This ties the choice of
K with the maximum achievable throughput. In our setting K = 32
and coding takes on average 270µs per 1500B packet. This limits the
effective throughput to 44 Mb/s, which is higher than the effective
bit rate of current wireless mesh networks [20].
(b) Memory Overhead: In MORE, like in ExOR, routers do not keep
an output queue. Instead, they store the current batch from each ﬂow.
This per-ﬂow state is dominated by the storage required to buffer
innovative packets from the current batch, which is bounded by
K = 32 packets. Additionally, as stated above, MORE nodes keep
a 64KiB lookup-table. Given that the number of concurrent ﬂows
in a mesh network is relatively small, we believe MORE’s memory
overhead is acceptable.
(c) Header Overhead: MORE’s header in our current implementa-
tion is bounded by 70 bytes because we bound the number of for-
warders to 10. Certain values in the header are compressed to in-
crease efﬁciency. For example, since routers only keep the current
batch, we can represent batch IDs using a few bits. Similarly, we
compress the node ID in the forwarder list to one byte, which is a
hash of its IP. This works because only nodes whose ETX to the
destination is smaller than the source are allowed to participate in
forwarding. For 1500B packets, the header overhead is less than 5%.
Note that our throughput numbers are computed over the delivered
data, and thus they already account for header overhead.
Note that the probe packets used to measure link loss probabilities
do not constitute a MORE-speciﬁc overhead. These probabilities are
measured by the all state-of-art wireless routing protocols, including
ExOR [7], and best-path [6].
9. C ONCLUSION
Opportunistic routing and network coding are two powerful ideas
which may at ﬁrst sight appear unrelated. Our work combines these

Throughput Dropoff
• Only every third node can transmit, or you get the
hidden terminal problem
• In TCP , data and ack packets cause the hidden
terminal problem
ABCD
ABC
datadata
dataack

Bidirectional Network Coding (COPE, Katti
et al.)

Coding
• Reed-Solomon codes for burst errors on small data
units
• LT codes for data delivery
• MORE for wireless communication
• General theme: being robust to individual losses
through mixing data and redundancy
• Layer 1 (Reed-Solomon), Layer 2.5 (MORE, COPE),
Layer 7 (LT)
