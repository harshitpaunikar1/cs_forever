Title: l11.pdf
Mapped Topic: Network systems course notes
Source URL: https://www.scs.stanford.edu/10au-cs144/notes/l11.pdf
Source Type: university_course_notes
Trust Score: 95
Fetched At: 2026-04-17T06:56:53+00:00
Mapped From CSE.md Section: Part 1 / Part 2.B

# Content

Lecture 11: Wireless Networking

Outline
• Wireless physical layer challenges
- Signal, noise, modulation
- A little bit of EE goes a long way
• Wireless link layers
- Hidden terminals, exposed terminals
- CSMA/CA
- RTS/CTS
• Wireless routing and throughput

Ethernet: 802.3
• Dominant wired LAN technology
- 10BASE5 (vampire taps)
- 10BASE-T, 100BASE-TX, 1000BASE-T
• Frame format:
PreambleType/LenPayload7 x 10101010SFD10101011Src6 bytes2 bytes46-1500 bytesCRC4 bytesGap96 ns,960 ns,9600 ns
PhysicalLinkLinkLayer 3Dest6 bytes

Physical Layer (Layer 1)
• Responsible for specifying the physical medium
- Category 5 cable (Cat5): 8 wires, twisted pair, RJ45 jack
- WiFi wireless: 2.4GHz
• Responsible for specifying the signal
- 100BASE-T: 5-level pulse amplitude modulation (PAM-5)
- 802.11b: Binary and quadrature phase shift keying
(BPSK/QPSK)
• Responsible for specifying the bits
- 100BASE-T: 4-to-6 bit-to-chip encoding, 3 chip symbols
- 802.11b: Barker code (1-2Mbps), complementary code
keying (5.5-11Mbps)

Wireless is Different
• Variable: signal attenuates over space
• Interference: other RF sources can interfere with
signal
• Multipath: signal can self-interfere
• Distributed: nodes cannot detect collisions
• To address these differences, wireless link layers
use slightly different mechanisms
• Also, can’t just abstract away the physical and link
layers: need a brief introduction to underlying EE

Attenuation Over Space
• Signal weakens as distance from transmitter
increases
• Reﬂections, obstructions, etc. complicate the
attenuation
• Depending on the antenna, not uniform in all
directions
• Much more complex than the wired model

Signal Strength Over Space

Directional Antennas

Interference
• In unlicensed bands (e.g., 802.11), there are lots of
transmitters
- 802.11 cards
- 802.15.1 (Bluetooth)
- 802.15.4 (ZigBee)
- 2.4GHz phones
- Microwave ovens
• This interference can be stronger or weaker than
the signal, and can prevent successful reception

Analog Signals
Amplitude
Wavelength

Specifying the Signal: Modulation
On-Off Keying(OOK)
101
Amplitude ShiftKeying (ASK)
101

Modulation, Continued
Frequency ShiftKeying (FSK)
101
Phase ShiftKeying (PSK)
101

I/Q Modulation
• I: in-phase, Q: quadrature
• Sum of two sines is a sine
• Show what the carrier looks like compared to a
simple, unmodulated signal
• Use I/Q because this is how it’s actually done in
hardware

I+Q

Modulation in I/Q Plots
QQQQIQ
OOKASKFSKBPSKQPSK

Example measurements from 16-QAM

Signal, Noise, and Interference
• Signal: energy of desired transmission
• Noise/Noise ﬂoor: energy of hardware thermal
effects
• Interference: energy of other transmitters
• Usually measured in dBm/dBW: 0dBm = 1mW,
0dBW = 30dBm = 1W
- Note dB is a logarithmic scale: 10dBm = 10mW, 20dBm =
100mW

Signal Plus Noise

SINR
• Signal to Interference-and-Noise Ratio
• Measured in dB:
| S |
| N + I |
- S = -50dBm, N+I = -95dBm, SINR = 45dB
- S = -89dBm, N+I = -93dBm, SINR = 4dB
• SINR is particularly critical in wireless because of
attenuation over space

Bit Error Rates
• There is a theoretical limit on how much
information a channel can carry (Shannon limit)
• Bit error rate depends on the SINR and the
modulation
• This is why wireless link layers use more complex
chip/bit encoding
- If signal is strong (high SINR), have few chip errors, can use
low encoding
- If signal is weak (low SINR), have many chip errors, use
higher encoding to recover from errors

Example Theoretical Bit Error Rates
2-3
After the signal is received and digitized, it is fed through a
series of adaptive delay stages which are summed together
via feedback loops. This technique is particularly effective in
slowly changing environments such as transmission over
telephone lines, but is more difﬁcult to implement in rapidly
changing environments like factory ﬂoors, ofﬁces and homes
where transmitters and receivers are moving in relation to
each other. The main drawback is the impact on system cost
and complexity. Adaptive equalizers can be expensive to
implement for broadband data links.
Spread spectrum systems are fairly robust in the presence
of multipath. Direct Sequence Spread Spectrum (DSSS)
systems will reject reﬂected signals which are signiﬁcantly
delayed relative to the direct path or strongest signal. This is
the same property which allows multiple users to share the
same bandwidth in Code Diversity Multiple Access (CDMA)
systems. Frequency Hopping Spread Systems (FHSS) also
exhibit some degree of immunity to multipath. Because a
FHSS transmitter is continuously changing frequencies, it
will always hop to some frequencies which experience little
or no multipath loss. In a severe fading environment,
throughput of an FHSS system will be reduced, but it is
unlikely that the link will be lost completely. The performance
of DSSS systems in the presence of multipath is described
further in a separate section below.
Modulation Technique
Modulation technique is a key consideration. This is the
method by which the analog or digital information is
converted to signals at RF frequencies suitable for
transmission. Selection of modulation method determines
system bandwidth, power efﬁciency, sensitivity, and
complexity. Most of us are familiar with Amplitude
Modulation (AM) and Frequency Modulation (FM) because
of their widespread use in commercial radio. Phase
Modulation is another important technique. It is used in
applications such as Global Position System (GPS)
receivers and some cellular telephone networks.
For the purposes of link budget analysis, the most important
aspect of a given modulation technique is the Signal-to-
Noise Ratio (SNR) necessary for a receiver to achieve a
speciﬁed level of reliability in terms of BER. A graph of E
b/No
vs BER is shown in Figure 4. Eb/No is a measure of the
required energy per bit relative to the noise power. Note that
E
b/No is independent of the system data rate. In order to
convert from Eb/No to SNR, the data rate and system
bandwidth must be taken into account as shown below:
where:
Eb = Energy required per bit of information
No= thermal noise in 1Hz of bandwidth
R = system data rate
B
T= system bandwidth
Spread Spectrum Radios
The term “spread spectrum” simply means that the energy
radiated by the transmitter is spread out over a wider amount
of the RF spectrum than would otherwise be used. By
spreading out the energy, it is far less likely that two users
sharing the same spectrum will interfere with each other.
This is an important consideration in an unlicensed band,
which why the regulatory authorities imposed spread
spectrum requirements on radios which transmit over -1dBm
(about 0.75mW) in the following bands:
FIGURE 3. ADAPTIVE EQUALIZER
∑
W1 W2 W3 W4 Wn
Z-1 Z-1 Z-1 Z-1
DIGITAL EQUALIZER OUT
DIGITIZED
BASEBAND
INPUT
TABLE 1. TYPICAL BANDWIDTHS FOR VARIOUS DIGITAL
MODULATION METHODS
MODULATION METHOD
TYPICAL BANDWIDTH
(NULL-TO-NULL)
QPSK, DQPSK 1.0 x Bit Rate
MSK 1.5 x Bit Rate
BPSK, DBPSK, OFSK 2.0 x Bit Rate
FIGURE 4. PROBABILITY OF BIT ERROR FOR COMMON
MODULATION METHODS
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
Eb/No (dB)
1.0E-01
1.0E-02
1.0E-03
1.0E-04
1.0E-05
1.0E-06
1.0E-07 BE
INCOHERENT OOK, OFSK
COHERENT OOK, OFSK
DBPSK, DQPSK
MSK, PSK
(EQ.4)SNR = (Eb/No) * (R/BT)
Application Note 9804

Variable Bit Rates
• 802.11b supports 1, 2, 5.5, and 11Mbps
• 2, 5.5Mbps and 11Mbps are QPSK
• To support this, the signal ﬁeld says what the data
rate is
- 00001010: 1Mbps (11 chips/bit, barker code)
- 00010100: 2Mbps (11 chips/bit, barker code)
- 00110111: 5.5Mbps (2 chips/bit, CCK)
- 01101110: 11Mbps (1 chip/bit, CCK)
• So the header is still at 1Mbps, even if the data is
at 11Mbps

Collisions are not so simple
ABC-40dB-60dB
• If A transmits ﬁrst, B can still decode its packet
• If C transmits ﬁrst, A will corrupt its packet and B
can’t decode C’s packet
• What if AB and BC are both -60dB?
• Signal strength matters: this is the RF capture
effect

802.11 Packet Loss Rates

802.11 Packet Loss Rates (at 11Mbps)
0.0
0.2
0.4
0.6
0.8 1.0
Packet Reception Ratio
0%
20%
40%
60%
80%
100%% Links
• How does this affect TCP?

Wireless PHY Summary
• Can’t control or limit the channel
• Need to deal with weak signals, interference, etc.
• Signal strength affects collisions
• Many different kinds of modulation: amplitude,
frequency, phase
• Use robust encodings when needed, use fast
speeds when possible
• Lots of intermediate packet delivery ratios

2 minute break

Wireless Link Layers

MAC Layer Responsibilities
• Arbitrate control of the channel
• One node should be able to use 100%
• Multiple nodes should get a fair share
• Want high utilization under contention

CA versus CD
• Collision detect (CD) is hard in wireless
• Local signal is much stronger than anything
received
• Protocols use collision avoidance (CA) by sensing
the channel

Simple MAC: CSMA/CA
• 1) Wait a small random period, check the channel
• 2) If the channel is busy, go to 1 (maybe longer
wait)
• 3) Transmit packet
B1B2B3B4, TXS

802.11b MAC: CSMA/CA
• Maintain a waiting counter c
• For each time step channel is idle, c −−
• When c = 0 , transmit
• If packet is not acknowledged (layer 2), pick a new,
larger c
- Use lack of layer 2 ack as collision detect
B1, TXB2, ACKS

Problems with CSMA/CA
• Want to know state of channel at receiver, not
transmitter
• But wireless is not transitive!
- A hears B
- A hears C
- B and C may not hear each other
- B and C can only sense their channel, but need to know if
A’s channel is clear

Hidden Terminal Problem
BAC
• B and C can’t hear each other, A can hear both
• B and C sense a clear channel, transmit, and
collide at A
• B is a hidden terminal to C, and C is a hidden
terminal to B

Exposed Terminal Problem
BACD
• A transmits to B
• C hears the transmission, backs off, even if it
wants to transmit to D
• C is an exposed terminal to A’s transmission

RTS/CTS
• Request-to-send, Clear-to-send (RTS/CTS)
• Allows transmitter to check availability of channel
at receiver
• Transmitter sends an RTS
• If it hears a CTS, sends data
• If not, retries RTS some time later
• If you hear a CTS for someone else, don’t transmit

RTS
BACRTS

CTS
BACCTS

Data
BACData

Network Allocation Vector (NA V)
• 802.11b supports RTS/CTS
• NA V is data structure node uses to know when
channel may be clear
• NA V is in terms of time : variable bit rates, RTS,
etc.

RTS/CTS Beneﬁts
• Solves the hidden terminal problem (assuming
CTS not corrupted)
- In practice, not true: a node’s CTS can collide with another
node’s RTS
- In practice, can reduce but not solve the hidden terminal
problem on data
- Control packets still collide
• Improves data packet delivery ratio
• Does it solve the exposed terminal problem? What
about ACKs?
BACD

RTS/CTS Drawbacks
• 3 packets per packet: RTS/CTS/DATA (4-22%
overhead in 802.11b)
• RTS still go through CSMA: they can be lost
• CTS losses cause lengthy retries
• 33% of IP packets are TCP ACKs: is it worth it?
• In practice, WiFi doesn’t use RTS/CTS

802.11 Association
• Terminal hears beacon from AP (scan channels), or
sends a probe request
• Terminal sends an authentication request , AP sends
authentication response
- If security is enabled, use keys
- Also “null” authentication
• Terminal sends association request , AP sends
association response

Association Continued
IEEE
Std 802.11-2007 LOCAL AND METROPOLITAN AREA NETWORKS—SPECIFIC REQUIREMENTS
44 Copyright © 2007 IEEE. All rights reserved.
Installing the PTK, and where appl icable the GTK keys, causes the MAC to encrypt and decrypt all
subsequent MSDUs irrespective of their path through the controlled or uncontrolled ports.
Upon successful completion of the 4-Way Hands hake, the Authenticator and Supplicant have
authenticated each other; and the IEEE 802.1X Controlled Ports are unblocked to permit general data traffic.
See Figure 5-13.
Figure 5-11—Establishing the IEEE 802.11 association
Figure 5-12—IEEE 802.1X EAP authentication
Supplicant Authenticator AS
802.1X EAP Request
802.1X EAP Response
EAP Authentication Protocol
Exchange
802.1X EAP Success
Accept / EAP Success /
Key Material
Access Request (EAP Request)
IEEE 802.1X
Controlled Port
Blocked for STA

2.4GHz Band

Wireless Routing

Wireless Routing
• Network is much more dynamic
• Not constrained by physical topology
• Discovering and estimating links to neighbors
• Discovering and maintaining routes to nodes
• Rich area of study: we’ll just touch on link cost

Hopcount Considered Harmful
• Minimizing hopcount causes protocol to choose
long links
• Links are more likely to be on edge of SNR/PRR
curve
- Less stable
- Require more maintenance
• One way wireless routing is different
• OLSRv2 adds the concept of link metrics

DSDV and Hopcount on Roofnet
0
0.2
0.4
0.6
0.8
1
0 50 100 150 200 250 300 350 400 450
Cumulative fraction of node pairs
Packets per second delivered
Run R1: 1 mW, 134-byte packets
Max 4-hop
throughput
2-hop3-hop
Best static route
DSDV hopcount
Figure 2: When using the minimum hop-count metric, DSDV
chooses paths with far less throughput than the best available
routes. Each line is a throughput CDF for the same 100 ran-
domly selected node pairs. The left curve is the throughput
CDF of DSDV with minimum hop-count. The right curve is
the CDF of the best throughput between each pair, found by
trying a number of promising paths. The dotted vertical lines
mark the theoretical maximum throughput of routes of each
hop-count.
and with a penalty to reﬂect the reduction in throughput caused by
interference between successive hops of multi-hop paths. New link
measurements were collected roughly every hour during the exper-
iment; the best paths for each pair were generated using the most
recently available loss data.
The values in Figure 2 are split into two main ranges, above and
below 225 packets per second. The values above 225 correspond to
pairs that communicated along single-hop paths; those at or below
225 correspond to multi-hop paths. A single-hop direct route can
deliver up to about 450 packets per second, but the fastest two-hop
route has only half that capacity. The halving is due to transmis-
sions on the successive hops interfering with each other: the middle
node cannot receive a packet from the ﬁrst node at the same time
it is sending a packet to the ﬁnal node. Similar effects cause the
fastest three-hop route to have a capacity of about 450/ 3 = 150
packets per second.
Minimum hop-count performs well whenever the shortest route
is also the fastest route, especially when there is a one-hop link with
a low loss ratio. A one-hop link with a loss ratio of less than 50%
will outperform any other route. This is the case for all the points
in the right half of Figure 2. Note that the overhead of DSDV route
advertisements reduces the maximum link capacity by about 15 to
25 packets per second, which is clearly visible in this part of the
graph.
The left half of the graph shows what happens when minimum
hop-count has a choice among a number of multi-hop routes. In
these cases, the hop-count metric usually picks a route signiﬁcantly
slower than the best known. The most extreme cases are the points
at the far left, in which minimum hop-count is getting a through-
put close to zero, and the best known route has a throughput of
0
50
100
150
200
23-19-24-36
23-37-24-36
23-37-19-36
23-12-19-36
23-19-11-36
23-19-36
23-19-20-36
23-19-7-36
Packets per second delivered
Run R1: 1 mW, 134-byte packets
Max 3-hop throughput
Max 4-hop
Figure 3: Throughput available between one pair of nodes, 23
and 36, along the best eight routes tested. The shortest of the
routes does not perform the best, and there are a number of
routes with the same number of hops that provide very differ-
ent throughput.
about 100 packets per second. The minimum hop-count routes are
slow because they include links with high loss ratios, which cause
bandwidth to be consumed by retransmissions.
2.3 Distribution of Path Throughputs
Figure 3 illustrates a typical case in which minimum hop-count
routing would not favor the highest-throughput route. The through-
put of eight routes from node 23 to node 36 is shown. The routes
are the eight best which were tested in the experiments described
above.
The graph shows that the shortest path, a two-hop route through
node 19, does not yield the highest throughput. The best route
is three hops long, but there are a number of available three-hop
routes which provide widely varying performance.
A routing protocol that selects randomly from the shortest hop-
count routes is unlikely to make the best choice, particularly as the
network grows and the number of possible paths between a given
pair increases.
2.4 Distribution of Link Loss Ratios
Figure 4 helps explain why high-throughput paths are difﬁcult to
ﬁnd. Each vertical bar corresponds to the direct radio link between
a pair of nodes; the two ends of the bar mark the broadcast packet
delivery ratio in the two directions between the nodes. To measure
delivery ratios, each node took a turn sending a series of broadcast
packets for ﬁve seconds, and counted the number of packets that
the 802.11b hardware reported as transmitted. Packets contained
134 bytes of 802.11b data payload. Every other node recorded the
number of packets received. The delivery ratio from node X to each
node Y is calculated by dividing the number of packets received by
Y by the number sent by X. The loss ratio of a link is one minus
its delivery ratio. We use the term “ratio” instead of “rate” to avoid
confusion with throughput delivery rates, which are expressed in
packets per second.
Note that 802.11b broadcasts don’t involve acknowledgements
or retransmissions. Because 802.11b retransmits lost unicast pack-
ets, the unicast packet loss ratio as seen by higher layers is far lower
than the underlying loss ratio (depending on the maximum number
of retransmissions allowed).
Three features of Figure 4 are important. First, a large fraction
of the links have an intermediate delivery ratio in at least one di-
rection. That is, they are likely to deliver some routing protocol
• From DeCouto et al., “A High-Throughput Path
Metric for Multi-Hop Wireless Routing.”

Variations Across Hopcounts
0
0.2
0.4
0.6
0.8
1
0 50 100 150 200 250 300 350 400 450
Cumulative fraction of node pairs
Packets per second delivered
Run R1: 1 mW, 134-byte packets
Max 4-hop
throughput
2-hop3-hop
Best static route
DSDV hopcount
Figure 2: When using the minimum hop-count metric, DSDV
chooses paths with far less throughput than the best available
routes. Each line is a throughput CDF for the same 100 ran-
domly selected node pairs. The left curve is the throughput
CDF of DSDV with minimum hop-count. The right curve is
the CDF of the best throughput between each pair, found by
trying a number of promising paths. The dotted vertical lines
mark the theoretical maximum throughput of routes of each
hop-count.
and with a penalty to reﬂect the reduction in throughput caused by
interference between successive hops of multi-hop paths. New link
measurements were collected roughly every hour during the exper-
iment; the best paths for each pair were generated using the most
recently available loss data.
The values in Figure 2 are split into two main ranges, above and
below 225 packets per second. The values above 225 correspond to
pairs that communicated along single-hop paths; those at or below
225 correspond to multi-hop paths. A single-hop direct route can
deliver up to about 450 packets per second, but the fastest two-hop
route has only half that capacity. The halving is due to transmis-
sions on the successive hops interfering with each other: the middle
node cannot receive a packet from the ﬁrst node at the same time
it is sending a packet to the ﬁnal node. Similar effects cause the
fastest three-hop route to have a capacity of about 450/ 3 = 150
packets per second.
Minimum hop-count performs well whenever the shortest route
is also the fastest route, especially when there is a one-hop link with
a low loss ratio. A one-hop link with a loss ratio of less than 50%
will outperform any other route. This is the case for all the points
in the right half of Figure 2. Note that the overhead of DSDV route
advertisements reduces the maximum link capacity by about 15 to
25 packets per second, which is clearly visible in this part of the
graph.
The left half of the graph shows what happens when minimum
hop-count has a choice among a number of multi-hop routes. In
these cases, the hop-count metric usually picks a route signiﬁcantly
slower than the best known. The most extreme cases are the points
at the far left, in which minimum hop-count is getting a through-
put close to zero, and the best known route has a throughput of
0
50
100
150
200
23-19-24-36
23-37-24-36
23-37-19-36
23-12-19-36
23-19-11-36
23-19-36
23-19-20-36
23-19-7-36
Packets per second delivered
Run R1: 1 mW, 134-byte packets
Max 3-hop throughput
Max 4-hop
Figure 3: Throughput available between one pair of nodes, 23
and 36, along the best eight routes tested. The shortest of the
routes does not perform the best, and there are a number of
routes with the same number of hops that provide very differ-
ent throughput.
about 100 packets per second. The minimum hop-count routes are
slow because they include links with high loss ratios, which cause
bandwidth to be consumed by retransmissions.
2.3 Distribution of Path Throughputs
Figure 3 illustrates a typical case in which minimum hop-count
routing would not favor the highest-throughput route. The through-
put of eight routes from node 23 to node 36 is shown. The routes
are the eight best which were tested in the experiments described
above.
The graph shows that the shortest path, a two-hop route through
node 19, does not yield the highest throughput. The best route
is three hops long, but there are a number of available three-hop
routes which provide widely varying performance.
A routing protocol that selects randomly from the shortest hop-
count routes is unlikely to make the best choice, particularly as the
network grows and the number of possible paths between a given
pair increases.
2.4 Distribution of Link Loss Ratios
Figure 4 helps explain why high-throughput paths are difﬁcult to
ﬁnd. Each vertical bar corresponds to the direct radio link between
a pair of nodes; the two ends of the bar mark the broadcast packet
delivery ratio in the two directions between the nodes. To measure
delivery ratios, each node took a turn sending a series of broadcast
packets for ﬁve seconds, and counted the number of packets that
the 802.11b hardware reported as transmitted. Packets contained
134 bytes of 802.11b data payload. Every other node recorded the
number of packets received. The delivery ratio from node X to each
node Y is calculated by dividing the number of packets received by
Y by the number sent by X. The loss ratio of a link is one minus
its delivery ratio. We use the term “ratio” instead of “rate” to avoid
confusion with throughput delivery rates, which are expressed in
packets per second.
Note that 802.11b broadcasts don’t involve acknowledgements
or retransmissions. Because 802.11b retransmits lost unicast pack-
ets, the unicast packet loss ratio as seen by higher layers is far lower
than the underlying loss ratio (depending on the maximum number
of retransmissions allowed).
Three features of Figure 4 are important. First, a large fraction
of the links have an intermediate delivery ratio in at least one di-
rection. That is, they are likely to deliver some routing protocol
• From DeCouto et al., “A High-Throughput Path
Metric for Multi-Hop Wireless Routing.”

Expected Transmissions (ETX)
• Proposed by DeCouto et al.
• Alternative metric: ETX, number of transmissions
until you receive an ACK
• Cost of link is
1
P RR AB · ARR BA
- P RR AB = 75% , ARR BA = 66% , ET X AB = 2 . 0
- P RR AB = 50% , ARR BA = 50% , ET X AB = 4 . 0
• Cost of route is sum of ETX values of links on
route

ETX Beneﬁts
0
0.2
0.4
0.6
0.8
1
0 50 100 150 200 250 300 350 400 450
Cumulative fraction of node pairs
Packets per second delivered
Run R1: 1 mW, 134-byte packets
Max 4-hop
throughput
2-hop3-hop
Best static route
DSDV ETX
DSDV Hop-count
Figure 6: ETX ﬁndshigher throughput routes than minimum
hop-count. This data is taken from the same experimental run
as Figure 2. Each point represents one of 100 node pairs.
In DSR experiments with ETX or minimum hop-count, a source
starts by sending one data packet per second for ﬁve seconds. This
ensure that DSR ﬁnds a route before throughput measurements are
taken. After the ﬁve seconds passes, the source sends packets as
fast as possible for 30 seconds. In DSR experiments with ETX, the
source waits an additional 15 seconds before initiating the route
request, to give the nodes time to accumulate link measurements.
All experiments run with the appropriate routing overhead. That
is, while measuring the throughput of routing with the ETX met-
ric, nodes send periodic ETX broadcast probes. While measuring
the throughput of DSDV (with either metric), nodes sends DSDV
routing advertisements, just as a production routing system would.
5.1 Metric Performance with DSDV
Figure 6 compares the throughput CDFs of paths found by DSDV
using ETX and minimum hop-count, between 100 randomly cho-
sen node pairs. This data is taken from the same run as in Figure 2,
and shows that DSDV using the ETX metric often ﬁnds much faster
routes than the minimum hop-count metric.
There are two main regions in Figure 6. The right half shows
node pairs that could communicate directly, with loss ratios less
than about 50% (i.e. with throughput greater than the maximum
possible two-hop throughput of 225 packets per second). In these
cases the minimum hop-count metric ﬁnds the one-hop route, which
is the best route, and there is no opportunity for ETX to perform
better. The left half corresponds to node pairs with a high direct
loss ratio, for which the best route has more than one hop. In this
region, the sensitivity of ETX to differences among the many dif-
ferent paths of the same length allows it often to ﬁnd better paths
than hop-count.
Figure 7 shows the same data as Figure 6, but organized as a
scatter plot to allow a direct comparison between the performance
of each metric for individual pairs. Each pair is represented by
one point; the point’s y value is the throughput obtained by DSDV
using ETX, and the x value is the throughput obtained by DSDV
using minimum hop-count. The upper-right quadrant shows pairs
where ETX and minimum hop-count both used the one-hop path.
0
50
100
150
200
250
300
350
400
450
0 50 100 150 200 250 300 350 400 450
DSDV ETX packets per second
DSDV Hop-count packets per second
Run R1: 1 mW, 134-byte packets
y=x
Figure 7: The ETX and hop-count data from Figure 6, plotted
on a per-pair basis. The x value of each point shows that pair’s
throughput for DSDV with minimum hop-count; the y value
shows the throughput for DSDV with ETX. Points above the
line y = x are pairs where ETX outperformed hop-count.
ETX outperforms minimum hop-count by the greatest margin
when the hop-count metric uses links with very asymmetric loss
ratios. This is illustrated by the points with x near zero and with
y relatively large. Minimum hop-count is using links that deliver
routing updates in one direction but deliver few or no data packets
in the other, while ETX correctly avoids those links.
The points for two pairs in Figure 7 lie well below the y = x
line; this is because of variations in link quality between the ETX
and minimum hop-count tests for those pairs. For the ﬁrst pair, both
ETX and hop-count used the same route, so the difference is due
to an underlying change in the route’s throughput. For the second
pair, ETX used a slower 3-hop path while hop-count used a two-
hop path; ETX avoided using one of the links in the two-hop path
because the measured delivery ratios were very poor. It is likely that
the link’s quality was different for the ETX and hop-count tests.
ETX incurs more overhead than minimum hop-count, due to its
loss-ratio probes, but this overhead is small compared to the gains
in throughput that ETX provides. ETX found usable routes for
many pairs where minimum hop-count was delivering essentially
zero packets per second.
Figure 8 shows the throughput for packets with a 1,386-byte pay-
load. Although ETX still offers an improvement over minimum
hop-count, the gain is not as large as for small packets. This is be-
cause ETX is still using small probes to estimate the link metrics.
Since small packets are more likely to be delivered, ETX is incor-
rectly over-estimating the quality of each link and causing DSDV
to pick sub-optimal routes. For example, if the single-hop direct
route between two nodes has an ETX probe delivery rate of 51%,
ETX will use it; however, the delivery rate of 1,386-byte packets
on such a link is likely to be closer to 1%, so a route with more
but higher-quality links would have been preferable. However, the
small packets are still useful for detecting very asymmetric links,
which is why ETX’s gain over minimum is more pronounced to the
left of the graph, where hop-count used very asymmetric links.
• From DeCouto et al., “A High-Throughput Path
Metric for Multi-Hop Wireless Routing.”

ETX Is Not Enough
• 802.11b supports four different bit rates
• ETX can select the route, but not the bitrate
• One packet at 11Mbps ̸= one packet at 1Mbps
• Solution: Estimated Time of Transmission (ETT)
- Probe at different bit rates
- Choose link bit rate based on minimum cost

Link Metrics Today
• Rough consensus that ETX/ETT is the right metric
- Addresses intermediate links
- Can be used across link layers
• No consensus on how to estimate the value
- Several proposals
- Still an active area of research
• Issue: conﬂates hopcount and link quality, making
loops very easy (100% → 33% can look like 2 more
hops)
• Issue: minimizes delay, does not maximize
throughput

Throughput Dropoff
• Only every third node can transmit, or you get the
hidden terminal problem
• In TCP , data and ack packets cause the hidden
terminal problem
ABCD
ABC
datadata
dataack

Wireless Routing
• Maintaining consistent, distributed state on a
dynamic system
• Preventing loops via serialization or source
routing
• On-demand versus continuous
• ETX/ETT better metric than hopcount
