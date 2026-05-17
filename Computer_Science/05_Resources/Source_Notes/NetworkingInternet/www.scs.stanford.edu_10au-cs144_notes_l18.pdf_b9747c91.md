Title: l18.pdf
Mapped Topic: Network systems course notes
Source URL: https://www.scs.stanford.edu/10au-cs144/notes/l18.pdf
Source Type: university_course_notes
Trust Score: 95
Fetched At: 2026-04-17T06:59:07+00:00
Mapped From CSE.md Section: Part 1 / Part 2.B

# Content

Course Survey
•Will be handed out after Thursday lecture
•Worth 3 extra credit points on ﬁnal exam
•SCPD: email to Alexis Wing
<alexisw@cs.stanford.edu>
‣She will anonymize answers, track who answered

Talk on Net Neutrality
•Barbara van Schewick on Internet
Architecture, Innovation and Network
Neutrality
‣Wednesday, December 1, 6-8PM
‣Stanford Law School, Room 290
‣http://cyberlaw.stanford.edu/node/6557
“T oday – following housing bubbles, bank collapses, and high
unemployment – the Internet remains the most reliable and
fantastic mechanism for fostering innovation and creating new
wealth. But this engine of innovation is under threat.”

Wireless Routing and
Full Duplex Wireless
Philip Levis
Stanford University
@CS144, 30.xi.2010
also Kyle Jamieson, Rodrigo Fonseca, Omprakash Gnawali, David Moss, Kannan Srinivasan,
Mayank Jain, Jung Il Choi, Maria Kazandjieva, Tal Rusak, and Sachin Katti.
3

?
Problem: deliver a packet to a destination across a multihop wireless network
Goal: minimize cost (transmissions/delivery)
Caveat: commodity wireless in unlicensed bands (802.11, 802.15.4, etc.)
S
D

S
D

S
D

S
D

S
D

Wireless Routing T oday(e.g., srcr[1])
•Links are not binary: good, bad, etc.
•Each node sends periodic (15s) beacons
‣Measures packet reception ratio (PRR)
‣Sliding 20 packet window (5 minutes)
•Compute costs of edges using PRR
‣Expected transmissions (ETX), PRR-1
•Use standard shortest path algorithms
[1] Bicket et al. “Architecture and Evaluation of an Unplanned 802.11b Mesh Network.” ACM Mobicom 2005

courtesy of Meraki.com
Free the Net, San Francisco
Purple tabs are wired gateways; green nodes provide multihop access
Numbers are hopcount from closest gateway
Lines show links

A Real Network: SWAN
Gates Packard
The Stanford Wireless Access Network (SWAN)
is an 802.11b/g testbed at Stanford. It is part of a
research collaboration with King Abdullah
University of Science and T echnology (KAUST).
2.5 seconds

A Real Network: SWAN
Gates Packard
The Stanford Wireless Access Network (SWAN)
is an 802.11b/g testbed at Stanford. It is part of a
research collaboration with King Abdullah
University of Science and T echnology (KAUST).
2.5 seconds

Long-term Link Behavior (scaling)
802.15.4 in Gates
802.11b in Free the Net
Bursts exist at time scales from seconds to months

Long-term Link Behavior (scaling)
•Red shows percentage of links that
exhibit behavior consistent with scaling
•No characteristic burst length
•8-53% of links
•Common across a wide range of
networks and durations
seconds to hours
minutes to days
hours to months
       
      E

Routing Summary
•Y ou can’t estimate link futures (scaling)
•Three mechanisms to route in this world
‣4-bit link estimation
‣Datapath validation
‣Adaptive beaconing

Link Estimation (4B)
S
D
df
dr
ETX = (df x dr)-1
Measuring df and dr with infrequent
beacons can be highly inaccurate.
Lines show percentile errors.
1.5
2
2.5
3
1.5 2 2.5 3
Average Cost (xmits/packet)
Average Tree Depth (hops)
White/Compare BitsAck Bit: Unidir. Est.
Ack Bit: Unidir. Est.
White/Compare Bits
4B
CTP + white bit
CTP + unidir
CTP T2
MultiHopLQI
Cost = Depth
45%
Directly measuring ETX with the data
path reduces path costs by 45%.
This requires a routing protocol can
adapt to such rapid edge cost changes.
Common Approach
ETXt = α⋅ETXt-1 + (1-α)Et
Et = 5acked
consecutive
unacked
{acked > 0
acked = 0
4-Bit estimator
every 5 packets,

Distance Vector Routing
A
NeighborRouteLink
A 5 2
D 5 2
F 2 1
J 3 3
C→H:
B
E
C
D
F
G
H
I
3
2
5
5
2
2
1
3

Distance Vector Challenges and Tradeoffs
S
1
S
2
D
2
2
10
D: 2
S2: 4
t=0

Distance Vector Challenges and Tradeoffs
S
1
S
2
D
2
2
10
D: 2
S2: 4
t=0 t=1
20
S
1
S
2
D2
10
S1: 6
S2: 4

Distance Vector Challenges and Tradeoffs
S
1
S
2
D
2
2
10
D: 2
S2: 4
t=0 t=1
20
S
1
S
2
D2
10
S1: 6
S2: 4
t=2
20
S
1
S
2
D2
10
S1: 6
S2: 8

Distance Vector Challenges and Tradeoffs
S
1
S
2
D
2
2
10
D: 2
S2: 4
t=0 t=1
20
S
1
S
2
D2
10
S1: 6
S2: 4
t=2
20
S
1
S
2
D2
10
S1: 6
S2: 8
t=4
20
S
1
S
2
D2
10
S1: 12
D: 10
Distance vector’s limited view of the network can
lead to long-lasting loops.
Rapid link cost changes exacerbate this problem.

Datapath Validation
A routing topology is consistent if
cost decreases on each hop.
Each data packet has a node’s cost:
the next hop checks consistency.
P
C
Reserved
THL
ETX
Origin
Seq. No.
Data packet header
A
B
C
D
01.42.54.1
1.41.11.6 Consistent
A
B
C
D
03.32.54.1
3.31.11.6 Inconsistent
A
B
C
D
03.34.44.1
3.31.11.6
3.3
Mid-repair
0
10
20
30
40
50
60
0 1 2 3 4 5 6 7
Node id
Time(hours)
Burst of inconsistencies as
topology repairs itself.

Adaptive Beaconing
P
C
Reserved
Parent
ETX
Нl
Нh
= 64ms
= 1 hour
Send control packets on a dynamic timer. Reset the timer to a
small value on three conditions:
1. Datapath validation detects an inconsistency
2. Receiving a packet with the Pull bit set
3. ETX decreases signiﬁcantly
Otherwise increase the beacon timer exponentially, up to a
max .
Control packet header
0
0.2
0.4
0.6
0.8
1
0 20 40 60 80 100 120 140
Delivery Ratio
Time(minutes)
maxmedianmin
Adaptive beaconing quickly
and seamlessly adapts to
large, correlated failures.
Adaptive beaconing sends 1/4 the
beacons of a 30 ﬁxed interval, while
reducing response time by 99.8%.
Нh
Нl

Further Systems Issues
S
Bs1,2,3
D
A
C
s2
s4
S
B
D
A
C
s4
s2
S
B
D
A
C
s2
s4
Packet duplication
a2 a1 a1
A
B
C
D
Self-interference
Link
Client QueuesPool
Link
Transmit Cache
?duplicate?
Transmit TimerSend Queue
CTP Forwarding
Path Design

CTP Noe Results Summary
Testbed Frequency MAC IPIDelivery5% Delivery Loss
Motelab 2.48GHz CSMA 16s 94.7% 44.7% Retransmit
Motelab 2.48GHz BoX-50ms 5m 94.4% 26.9% Retransmit
Motelab 2.48GHz BoX-500ms 5m 96.6% 82.6% Retransmit
Motelab 2.48GHz BoX-1000ms 5m 95.1% 88.5% Retransmit
Motelab 2.48GHz LPP-500ms 5m 90.5% 47.8% Retransmit
T utornet (26) 2.48GHz CSMA 16s 99.9% 100% Queue
T utornet (16) 2.43GHz CSMA 16s 95.2% 92.9% Queue
T utornet (16) 2.43GHz CSMA 22s 97.9% 95.4% Queue
T utornet (16) 2.43GHz CSMA 30s 99.4% 98.1% Queue
Wyman Park 2.48GHz CSMA 16s 99.9% 100% Retransmit
NetEye 2.48GHz CSMA 16s 99.9% 96.4% Retransmit
Kansei 2.48GHz CSMA 16s 99.9% 100% Retransmit
Vinelab 2.48GHz CSMA 16s 99.9% 99.9% Retransmit
Quanto 2.425GHz CSMA 16s 99.9% 100% Retransmit
T wist (Tmote) 2.48GHz CSMA 16s 99.3% 100% Retransmit
T wist (Tmote) 2.48GHz BoX-2s 5m 98.3% 92.9% Retransmit
Mirage (micaZ) 2.48GHz CSMA 16s 99.9% 99.8% Queue
Mirage (mica2dot) 916.4MHz B-MAC 16s 98.9% 97.5% Ack
T wist (eyesIFX) 868.3MHz CSMA 16s 99.9% 99.9% Retransmit
T wist (eyesIFX) 868.3MHzSpeckMAC-183ms 30s 94.8% 44.7% Queue
Blaze 315MHzB-MAC-300ms 4m 99.9% Queue

RPL

RPL(Routing Protocol for Low power and lossy networks)
•Proposed IETF standard for low-power and
lossy networks (LLNs), under IESG review
‣Smart meter networks
‣Home area networks
‣Sensor networks
‣The “Internet of Things”
•Core protocol is CTP Noe
‣Lots more details and mechanisms, of course

RPL Basics
A
B
E
C
D
F
G
H
I
DODAG Root
DODAG: Destination Oriented Directed Acyclic Graph
- A routing topology can have multiple DODAGs
- A node is a member of only one DODAG at any time
Neighbor set: subset of link-local neighbors
Parent set: subset of neighbors which have lower cost
Preferred parent: current next hop

RPL Basics
A
B
E
C F
G
I
DODAG Root
D
H
DODAG: Destination Oriented Directed Acyclic Graph
- A routing topology can have multiple DODAGs
- A node is a member of only one DODAG at any time
Neighbor set: subset of link-local neighbors
Parent set: subset of neighbors which have lower cost
Preferred parent: current next hop

RPL Basics
A
B
E
C F
G
I
DODAG Root
D
H
DODAG: Destination Oriented Directed Acyclic Graph
- A routing topology can have multiple DODAGs
- A node is a member of only one DODAG at any time
Neighbor set: subset of link-local neighbors
Parent set: subset of neighbors which have lower cost
Preferred parent: current next hop

RPL Basics
A
B
E
C F
G
I
DODAG Root
DODAG: Destination Oriented Directed Acyclic Graph
- A routing topology can have multiple DODAGs
- A node is a member of only one DODAG at any time
Neighbor set: subset of link-local neighbors
Parent set: subset of neighbors which have lower cost
Preferred parent: current next hop
D
H

More RPL Basics
Upward routes: routes toward a DODAG root
(decreasing cost)
Downward routes: routes away from a
DODAG root (increasing cost)
Rank: metric independent way to encode cost
A
B
E
C
F
GI
DODAG Root
D
H
Up
Down

RPL Messages
•Destination Information Object (DIO)
‣Upward routes
•Destination Advertisement Object (DAO),
DAO Acknowledgement (DAO-ACK)
‣Downward routes
•Destination Information Solicitation (DIS)
‣Discovery, conﬁguration
•Consistency Check (CC)
‣Security, protection against replay

DIO
DODAGID
RPLInstanceId
Version Number
Rank
G
0
MOP
Prf
DTSN
Flags
Reserved
DIOs spread down, establish upward routes
Sent on an exponential timer (like CTP Noe)

DIO Timer Reset
•On receiving a DIS message (like pull bit)
•On a new DODAG sequence number
•On datapath validation check failure
‣Rank encoded as an IPv6 hop-by-hop header

RPL Options
•Messages can include options
•Example: DODAG Conﬁguration Option
‣Included in DIO sent in response to DIS
DIOIntMin.
DIORedun.
A
Flags
PCS
DIOIntDoubl.
OCP
Lifetime Unit
MinHopRankIncrease
Reserved
Def. Lifetime
Type=4
Length=14
MaxRankIncrease

Wireless Routing Summary
•Wireless links are bursty and many exhibit scaling
•Fast link estimation critical: reduces costs by 45%
•Fast link estimators complicate routing
•CTP Noe: datapath validation and adaptive beacons
•Basis for proposed Internet standard RPL
37

Full Duplex Wireless

Problem with CTP Noe(not designed for high throughput)
Self-interference
Low power networks have light load.
But as load along a route increases,
self-interference increases link costs.
These changes follow the route: the
topology can become unstable and,
sometimes, collapse.
a2 a1 a1
A
B
C
D
Hidden terminals

40
“It is generally not possible for radios to receive
and transmit on the same frequency band because
of the interference that results. Thus, bidirectional
systems must separate the uplink and downlink
channels into orthogonal signaling dimensions,
typically using time or frequency dimensions.”
- Andrea Goldsmith, “Wireless Communications,” Cambridge Press, 2005.

Can a wireless node transmit AND
receive at the same time on a single band?
41

Can a wireless node transmit AND
receive at the same time on a single band?
42
Status quo: NO

43
Chuck Thacker InterviewCommunications of the ACM, July 2010

Why only half-duplex on a single band?
44

Why only half-duplex on a single band?
•Very strong self-interference
•~70dB stronger for 802.15.4
•Analog to Digital converter (ADC) saturates
TXRX
45
TXRX

•Digital cancellation: subtracting known interference
digital samples from received digital samples.
ZigZag[1], Analog Network Coding[2] etc.
•Hardware cancellation: RF noise cancellation circuits with
transmit signal as noise reference
Radunovic et al.[3]
Existing T echniques
46
[1] Gollakota et al. “ZigZag Decoding: Combating Hidden T erminals in Wireless Networks”, ACM SIGCOMM 2008
[2] Katti et al. “Embracing Wireless Interference: Analog Network Coding”, ACM SIGCOMM 2007
[3] Radunovic et al. , "Rethinking Indoor Wireless: Lower Power, Low Frequency, Full-duplex", WiMesh (SECON
Workshop),, 2010

•Digital cancellation: subtracting known interference
digital samples from received digital samples.
ZigZag[1], Analog Network Coding[2] etc.
Ineffective if ADC saturates
•Hardware cancellation: RF noise cancellation circuits with
transmit signal as noise reference
Radunovic et al.[3]
Existing T echniques
47
[1] Gollakota et al. “ZigZag Decoding: Combating Hidden T erminals in Wireless Networks”, ACM SIGCOMM 2008
[2] Katti et al. “Embracing Wireless Interference: Analog Network Coding”, ACM SIGCOMM 2007
[3] Radunovic et al. , "Rethinking Indoor Wireless: Lower Power, Low Frequency, Full-duplex", WiMesh (SECON
Workshop),, 2010

These are not enough: 25dB +15dB < 70dB
•Digital cancellation: subtracting known interference
digital samples from received digital samples.
ZigZag[1], Analog Network Coding[2] etc. ~15dB
Ineffective if ADC saturates
•Hardware cancellation: RF noise cancellation circuits with
transmit signal as noise reference
Radunovic et al.[3] ~25dB
Existing T echniques
48

Innovation: Antenna Cancellation
d d + λ/2
TX1 TX2RX
49

Innovation: Antenna Cancellation
~30dB self-interference cancellation
Enables full-duplex when combined with digital (15dB) and
hardware (25dB) cancellation.
d d + λ/2
TX1 TX2RX
50

Can a wireless node transmit AND receive
at the same time on a single band?
51

Can a wireless node transmit AND receive
at the same time on a single band?
YES, IT CAN!
Full-duplex prototype achieves 92% of the
throughput of an “ideal” full-duplex system
52

Three techniques give ~70dB cancellation
•Antenna Cancellation (~30dB)
•Hardware Cancellation (~25dB)
•Digital Cancellation (~15dB)
53

Our Prototype
54
Antenna
Cancellation
Hardware
Cancellation
Digital
Interference
Cancellation

Bringing It T ogether
QHX220
ADC
Hardware
Cancellation
TX Signal
Antenna
Cancellation
55
RX
Digital
Cancellation
∑TX Samples
+-
Clean RX samples
RF
Baseband

Bringing It T ogether
QHX220
ADC
Hardware
Cancellation
TX Signal
Antenna
Cancellation
56
RX
Digital
Cancellation
∑TX Samples
+-
Clean RX samples
RF
Baseband

Bringing It T ogether
QHX220
ADC
Hardware
Cancellation
TX Signal
Antenna
Cancellation
57
RX
Digital
Cancellation
∑TX Samples
+-
Clean RX samples
RF
Baseband

Bringing It T ogether
QHX220
ADC
Hardware
Cancellation
TX Signal
Antenna
Cancellation
58
RX
Digital
Cancellation
∑TX Samples
+-
Clean RX samples
RF
Baseband

-60
-55
-50
-45
-40
-35
-30
-25
0 5 10 15 20 25
RSSI (dBm)
Position of Receive Antenna (cm)
TX1 TX2
Only TX1 Active
Antenna Cancellation: Performance
59

-60
-55
-50
-45
-40
-35
-30
-25
0 5 10 15 20 25
RSSI (dBm)
Position of Receive Antenna (cm)
TX1 TX2
Only TX2 Active
Antenna Cancellation: Performance
60
Only TX1 Active

-60
-55
-50
-45
-40
-35
-30
-25
0 5 10 15 20 25
RSSI (dBm)
Position of Receive Antenna (cm)
TX1 TX2
Only TX1 Active
Only TX2 Active
Both TX1 &
TX2 Active
Antenna Cancellation: Performance
61
Null
Position

-60
-55
-50
-45
-40
-35
-30
-25
0 5 10 15 20 25
RSSI (dBm)
Position of Receive Antenna (cm)
TX1 TX2
Only TX1 Active
Only TX2 Active
Both TX1 &
TX2 Active
Antenna Cancellation: Performance
62
~25-30dBNull
Position

Sensitivity of Antenna Cancellation
63
Amplitude Mismatch
between TX1 and TX2
Placement Error
for RX
dB
Reduction Limit (dB) Reduction Limit (dB)
Error (mm)

Sensitivity of Antenna Cancellation
64
dB
Reduction Limit (dB) Reduction Limit (dB)
Error (mm)
30dB cancellation < 5% (~0.5dB) amplitude mismatch
< 1mm distance mismatch
Amplitude Mismatch
between TX1 and TX2
Placement Error
for RX

Sensitivity of Antenna Cancellation
65
dB
Reduction Limit (dB) Reduction Limit (dB)
Error (mm)
•Rough prototype good for 802.15.4
•More precision needed for higher power systems (802.11)
Amplitude Mismatch
between TX1 and TX2
Placement Error
for RX

Bandwidth Constraint
A λ/2 offset is precise for one frequency
66
fc
d d + λ/2
TX1 TX2RX

Bandwidth Constraint
A λ/2 offset is precise for one frequency
not for the whole bandwidth
67
fc fc+Bfc -B
d d + λ/2
TX1 TX2RX

Bandwidth Constraint
A λ/2 offset is precise for one frequency
not for the whole bandwidth
68
fc fc+Bfc -B
d d + λ/2
TX1 TX2RX
d2 d2 + λ+B/2
TX1 TX2RX
d1 d1 + λ-B/2
TX1 TX2RX

Bandwidth Constraint
69
fc fc+Bfc -B
d d + λ/2
TX1 TX2RX
d2 d2 + λ+B/2
TX1 TX2RX
d1 d1 + λ-B/2
TX1 TX2RX
WiFi (2.4G, 20MHz) => ~0.26mm precision error
A λ/2 offset is precise for one frequency
not for the whole bandwidth

Bandwidth Constraint
70
2.4 GHz
5.1 GHz
300 MHz

Bandwidth Constraint
71
2.4 GHz
5.1 GHz
300 MHz
•WiFi (2.4GHz, 20MHz): Max 47dB reduction
•Bandwidth‐ => Cancellation‑
•Carrier Frequency‐ => Cancellation‐

•802.15.4 based signaling on USRP nodes
•T wo nodes at varying distances placed in an
ofﬁce building room and corridor
Experimental Setup
72

•Full-duplex should double aggregate throughput
73
Half-Duplex :- Nodes interleave transmissions
Node 1 ➜ 2
Node 2 ➜ 1
Node 1 ➜ 2
Node 2 ➜ 1
Full-Duplex :- Nodes transmit concurrently

Median throughput 92% of ideal full-duplex
Throughput
0
0.2
0.4
0.6
0.8
1.0
050100150200250300
CDF
Throughput (Kbps)
Half-DuplexFull-DuplexIdeal Full-Duplex
1.84x
74

0
0.2
0.4
0.6
0.8
1.0
050100150200250300
CDF
Throughput (Kbps)
Throughput
Half-DuplexFull-DuplexIdeal Full-Duplex
1.84x
75
Performance loss
at low SNR

76
The prototype gives 1.84x throughput gain
with two radios compared to half-duplex
with a single radio.
So what? PHY gains similar to 2x2 MIMO
(and we need 3 antennas)

The prototype gives 1.84x throughput gain
with two radios compared to half-duplex
with a single radio.
So what? PHY gains similar to 2x2 MIMO
(and we need 3 antennas)
True beneﬁt lies beyond the physical layer
77

•Breaks a basic assumption in wireless
•Can we solve some fundamental problems
with wireless networks today?
•Hidden terminals
•Primary detection in whitespaces
•Network congestion and WLAN fairness
•Latency in multihop wireless
Implications to Wireless Networks
78

•CSMA/CA can’t solve this
•Schemes like RTS/CTS introduce signiﬁcant overhead
APN1 N2
Current networks have
hidden terminals
Mitigating Hidden T erminals
79

•CSMA/CA can’t solve this
•Schemes like RTS/CTS introduce signiﬁcant overhead
APN1 N2
Since both sides transmit at the same time, no
hidden terminals exist
Current networks have
hidden terminals
Full Duplex solves
hidden terminals
APN1 N2
Mitigating Hidden T erminals
80

Network Congestion and WLAN Fairness
Without full-duplex:
•1/n bandwidth for each node in network, including AP
Downlink Throughput = 1/n Uplink Throughput = (n-1)/n
81

Network Congestion and WLAN Fairness
Without full-duplex:
•1/n bandwidth for each node in network, including AP
Downlink Throughput = 1/n Uplink Throughput = (n-1)/n
82
With full-duplex:
•AP sends and receives at the same time
Downlink Throughput = 1 Uplink Throughput = 1

Long delivery and round-trip times in multi-
hop networks
Solution: wireless cut-through routing!
N1 N2 N3 N4
N1
N2
N3
N4
N1
N2
N3
N4
Time Time
Half-duplex
Time
Full-duplex
Reducing Round-Trip Times
83

Questions
84

Internet T oday
85

After CS144
86
CS140
(w)
CS240
(s)
CS244B
(s)
CS144
(f)
CS244
(w)
CS244E
(w)
CS344
(s)
CS344E
(s)
CS142
(f)
CS241
CS155
(s)
CS255
(w)
CS259
(w)
Networking
Systems
Web Applications
Security
advanced OS
distributed systems
general networking
wireless networking
cryptography
protocol security
secure web programming

Final Lecture
•Guest lecture: Jon Peterson
•On Internet Architecture Board (IAB)
•Co-chair of alto working group
•Co-author of Session Initiation Protocol (SIP)
•Will talk about alto and other issues in the
Internet today -- bring questions!
87

88

Backup
89

•Bandwidth Constraint
Working on a frequency independent technique
•Time-varying wireless channel
Auto-tuning of the hardware cancellation circuit
•Multi-path
Estimate and incorporate in digital cancellation: Some
existing work does this
•Single stream
Extension to MIMO-like systems
90

Summary
•Working prototype for achieving in-band full-
duplex wireless
•Cancellation limited by engineering precision and
bandwidth of channel
•Phase offset, amplitude, circuit noise
•How far can full duplex go? WiFi? WiMAX/LTE?
•As we add more antennas, what degrees of
freedom do we have and how should we use them?
•How does this change the rest of the stack?
91

92
What about attenuation at intended receivers?
Destructive interference can affect this signal too!

0102030-30-20-10
0
10
20
30
-30
-20
-10
x axis (meters)
y axis (meters)
93
Equal Transmit Power
Deep Nulls at 20-30m
Unequal Transmit Power
What about attenuation at intended receivers?
Destructive interference can affect this signal too!
•Different transmit powers for two TX helps
0102030-30-20-10
0
10
20
30
-30
-20
-10
x axis (meters)
y axis (meters)

0102030-30-20-10
0
10
20
30
-30
-20
-10
x axis (meters)
y axis (meters)
94
Equal Transmit PowerUnequal Transmit Power
0102030-30-20-10
0
10
20
30
-30
-20
-10
x axis (meters)
y axis (meters)
-52 dBm
-58 dBm-52 dBm -100 dBm
What about attenuation at intended receivers?
Destructive interference can affect this signal too!
•Different transmit powers for two TX helps

Little loss in link reliability: 88% of half-duplex on average
Link Reception Ratio
95
0
0.25
0.50
0.75
1.00
010203040
Packet Reception Ratio
SNR (dB)
Half-DuplexFull-Duplex

0
0.25
0.50
0.75
1.00
010203040
Packet Reception Ratio
SNR (dB)
Link Reception Ratio
Half-DuplexFull-Duplex
96
•Loss at High SNR: Due to spurious signal peaks in USRP
Loss at
High SNR

0
0.25
0.50
0.75
1.00
010203040
Packet Reception Ratio
SNR (dB)
Half-DuplexFull-Duplex
Link Reception Ratio
•Loss at High SNR: Due to spurious signal peaks in USRP
•Loss at low SNR: Due to imprecisions in prototype97
Loss at
Low SNR

Network Congestion and WLAN Fairness
Without full-duplex
•APs contend with clients for
wireless access
•Downlink throughput = 1/n
•Bottleneck at AP
For an AP serving many clients
t=0
t=1
t=2
t=3
98

Network Congestion and WLAN Fairness
Without full-duplex
•APs contend with clients for
wireless access
•Downlink throughput = 1/n
•Bottleneck at AP
Full-duplexing reduces congestion
•AP transmits and receives at the
same time
•Downlink = Uplink = 1
For an AP serving many clients
t=0
t=1
t=2
t=3
99

Primary Detection in Whitespaces
Secondary transmitters should not interfere with
primary transmissions
Time
Primary TX
(Broadcast TV) Secondary TX
(Whitespace transmitter)
Interference
100

Primary Detection in Whitespaces
Secondary transmitters should not interfere with
primary transmissions
Time
Primary TX
(Broadcast TV) Secondary TX
(Whitespace transmitter)
Interference
Primary TX
(Broadcast TV)
Primary sensing
101

Primary Detection in Whitespaces
Secondary transmitters should not interfere with
primary transmissions
Time
Primary TX
(Broadcast TV) Secondary TX
(Whitespace transmitter)
Interference
Primary sensing
Traditional nodes can’t send and sense at the same time
Primary TX
(Broadcast TV)
102

Primary Detection in Whitespaces
Time
Primary TX
(Broadcast TV) Secondary TX
(Whitespace transmitter)
Interference
Primary sensing
Traditional nodes can’t send and sense at the same time
Full-duplex nodes can
Secondary TX
(Whitespace transmitter)Primary TX
(Broadcast TV)
103

Primary Detection in Whitespaces
Secondary transmitters should sense for primary
transmissions before channel use
Time
104
Primary sensing
Primary TX
(Wireless Mics)
Secondary TX
(Whitespace AP)

Bringing It T ogether
Digital Interference
Cancellation
d d + λ/2 TX1 TX2RX
QHx220
RF Analog
RF ➔ BasebandADC
RF Analog
Baseband ➔ RF
DAC
EncoderDecoderDigital
Interference
Reference
Hardware Cancellation
TX Signal Path RX Signal Path
Antenna Cancellation
105

Bringing It T ogether
Digital Interference
Cancellation
d d + λ/2 TX1 TX2RX
QHx220
RF Analog
RF ➔ BasebandADC
RF Analog
Baseband ➔ RF
DAC
EncoderDecoderDigital
Interference
Reference
Hardware Cancellation
TX Signal Path RX Signal Path
Antenna Cancellation
106

Digital Interference
Cancellation
Bringing It T ogether
d d + λ/2 TX1 TX2RX
QHx220
RF Analog
RF ➔ BasebandADC
RF Analog
Baseband ➔ RF
DAC
EncoderDecoderDigital
Interference
Reference
Hardware Cancellation
TX Signal Path RX Signal Path
Antenna Cancellation
107

Median throughput 92% of ideal full-duplex
Throughput
108
0
0.25
0.50
0.75
1.00
00.20.40.60.811.21.41.61.82
1.84x

0
0.2
0.4
0.6
0.8
1.0
050100150200250300
CDF
Throughput (Kbps)
Throughput
Half-DuplexFull-DuplexIdeal Full-Duplex
1.84x
109
Performance loss at low SNR

Primary Detection in Whitespaces
Secondary transmitters should sense for primary
transmissions before channel use
Time
110
Primary TX
(Wireless Mics)
Secondary TX
(Whitespace AP)
Primary sensing
Primary TX
(Wireless Mics)
Secondary TX
(Whitespace AP)
Traditional nodes may still interfere during transmissions
Interference

Primary Detection in Whitespaces
Secondary transmitters should sense for primary
transmissions before channel use
Time
111
Primary sensing
Primary TX
(Wireless Mics)
Secondary TX
(Whitespace AP)
Full-duplex nodes can sense and send at the same time
Primary sensing
Primary TX
(Wireless Mics)
Secondary TX
(Whitespace AP)
