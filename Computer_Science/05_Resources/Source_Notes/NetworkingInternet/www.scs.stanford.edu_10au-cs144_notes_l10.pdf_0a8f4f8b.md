Title: l10.pdf
Mapped Topic: Network systems course notes
Source URL: https://www.scs.stanford.edu/10au-cs144/notes/l10.pdf
Source Type: university_course_notes
Trust Score: 95
Fetched At: 2026-04-17T06:56:38+00:00
Mapped From CSE.md Section: Part 1 / Part 2.B

# Content

Lecture 10: TCP Friendliness, DCCP , NATs,
and STUN

TCP Friendliness

Congestion Control
• TCP dynamically adapts its rate in response to
congestion
• AIMD causes ﬂows to converge to fair goodput
• But how do losses (e.g., bit errors) affect goodput?
• What about UDP?

Chiu Jain Phase Plots
Flow A rate (bps)
Flow B rate (bps)FairA=B
EfﬁcientA+B=C
overload
underload
t1
t2
t3
t4
t5
t6

Responding to Loss
• Set threshold to
cwnd
2
• On timeout
- Set cwnd to 1
- Causes TCP to enter slow start
• On triple duplicate ACK (Reno)
- Set cwnd to
cwnd
2
- Retransmit missing segment
- Causes TCP to stay in congestion avoidance

Analyzing TCP Simply
• Assume all segments are MSS long
• Assume a packet loss rate p
• Assume a constant RTT
• Assume p is small (no timeouts)

Analysis
• Window size W cuts to
W
2
after a loss
• Grows to W after
W
2
RTTs
• Goodput =
3
4
· W · M T U ·
1
RT T

Window Size
• p =
1
(
W
2
+(
W
2
+1)+ ... + W )
• p ≈
1
3
8
W 2
• W ≈
√
8
3 · p
• Goodput =
3
4
·
√
8
3 · p
· M T U ·
1
RT T
• Goodput =
1 . 22 · M T U
RT T ·
√
p
• Constant factor changes based on delayed acks,
etc.

TCP Friendliness
• Don’t want other protocols to disrupt TCP
• UDP happily shuts down TCP ﬂows
• “TCP friendliness:” obeying TCP congestion
control as per prior goodput equation
- Does not imply acting like TCP
- E.g., does not require abrupt window changes

ledbat WG
• “The LEDBAT WG is chartered to standardize a
congestion control mechanism that should saturate
the bottleneck, maintain low delay, and yield to
standard TCP .”
• TCP-friendliness is insufﬁcient for modern P2P
applications
- Flow fairness, not application fairness
- TCP ﬁlls queues
• Elastic workloads vs. inelastic workloads

DCCP

DCCP
• Datagram Congestion Control Protocol (DCCP)
provides congestion control for unreliable
datagrams (RFC 4340)
• Connection-oriented protocol
- Request-response-ack establishment
- Close-reset or CloseReq-Close-reset teardown
• Counts packets, not bytes

DCCP Segment

Sequence Numbers
• Every DCCP packet uses a new sequence number
- Data
- Acknowledgements
- Control trafﬁc
• Acknowledgements are for last packet received
- Not cumulative acknowledgements
- Does not succinctly describe connection history
- Options can give packet vectors

Synchronization
• DCCP uses sequence number windows to protect
from attacks
• Large bursts of losses cause packets to fall past
windows
• Need to resynchronize

Synchronization Exchange

Synchronization on Reset Problem

Synchronization on Reset Solution

Congestion Control
• Deﬁnes Congestion Control IDs (CCIDs)
• Negotiated with change/conﬁrm L/R options
• Each half-connection can have different
congestion control
• CCID 2: TCP congestion control (AIMD) (RFC
4941)
• CCID 3: TCP-friendly congestion control (RFC
4942)

CCID 2
• Uses TCP congestion control
- Maintains a cwnd , slow-start, etc.
• Adds congestion control to acks
- Sender speciﬁes an AckRatio , R
- Ratio of data to ack packets (TCP with delayed ACKs is 2)
- On detecting ack losses, double R
- After
cwnd
R
2
− R
lossless congestion windows, decrement R

CCID 3
• Uses TCP-friendly congestion control
• Uses a sending rate, rather than a congestion
window
• Receiver sends feedback once per RTT, reporting
loss rate
• If sender hears no feedback, halves sending rate
• Security issue with loss rate reporting: report loss
intervals , rather than just a loss rate, veriﬁable
with ECN nonces

DCCP Today
• Numerous implementations
• IETF Standards Track
• Well suited to VoIP , Internet Gaming, etc.
• Sees very little use

2-minute stretch

Network Address Translator

NAT
• Network Address Translator
NAT(128.34.22.8)
Client A(10.0.0.101)
NAT(76.18.117.20)
Client B(10.1.1.9)
Session A-S10.0.0.101:123418.181.0.31:22Session B-S10.1.1.9:541118.181.0.31:22
Server(18.181.0.31)Session B-S76.18.117.20:1000118.181.0.31:22Session A-S128.34.22.8:610118.181.0.31:22

Motivations and Complications
• There are only 2
32
IP addresses
• Firewalls for security
• Breaks end-to-end (node does not know its
external IP)
• Node might not even know if it’s behind a NAT
• NAT needs to be able to dynamically assign
mappings

How a NAT Works
• Maps between global and local (IP ,port) pairs
• Requires knowledge of transport packet format
• UDP datagram, TCP SYN
- Can shut down TCP mapping on FIN+ACK
- UDP requires timeouts ( > 2 minutes, unless IANA says
otherwise)
• RFC 4787/BCP 127 deﬁnes recommended
behaviors

NAT Example, Step 1
NAT(128.34.22.8)
Client A(10.1.1.18)Server(18.181.0.31)
Client B(10.1.1.9)

NAT Example, Step 2
NAT(128.34.22.8)
Client A(10.1.1.18)Server(18.181.0.31)
Client B(10.1.1.9)
10.1.1.1818.181.0.31451280
Client A tries to opena connection to Server port 80 from port 4512

NAT Example, Step 3
NAT(128.34.22.8)
Client A(10.1.1.18)Server(18.181.0.31)
Client B(10.1.1.9)
NAT rewrites the sourceaddress and port so itseems it is the source
128.34.22.818.181.0.3166418010.1.1.1818.181.0.31451280

NAT Example, Step 4
NAT(128.34.22.8)
Client A(10.1.1.18)Server(18.181.0.31)
Client B(10.1.1.9)
NAT also creates a mappingso it can transform futurepackets correctly
10.1.1.1818.181.0.314512128.34.22.8664180

NAT Example, Step 5
NAT(128.34.22.8)
Client A(10.1.1.18)Server(18.181.0.31)
Client B(10.1.1.9)
Server responds to SYNwith SYN+ACK and NATrewrites it
128.34.22.818.181.0.3166418010.1.1.1818.181.0.3145128010.1.1.1818.181.0.314512128.34.22.8664180

NAT Example, Step 6
NAT(128.34.22.8)
Client A(10.1.1.18)Server(18.181.0.31)
Client B(10.1.1.9)
Client B can also opena connection, and the NATcreates a mapping for it too
128.34.22.818.181.0.3140508010.1.1.1918.181.0.3199678010.1.1.1918.181.0.319967128.34.22.8405080

NAT Example, Step 7
Client A(10.1.1.18)Server(18.181.0.31)
In the case of TCP, NATcan discard the mappingon close or RST
NAT(128.34.22.8)
Client B(10.1.1.9)
128.34.22.818.181.0.3166418010.1.1.1818.181.0.3145128010.1.1.1818.181.0.314512128.34.22.8664180
RSTRST

Types of NAT (RFC 3849)
• Full Cone: no ingress ﬁlter (single local-external
mapping)
• Restricted Cone: ingress ﬁlter on address
• Port Restricted: ingress ﬁlter on address/port
• Symmetric: different mappings for different
external destinations
• Teminology is imperfect (static port mappings,
etc.)

NAT Problems
• Incoming TCP connections
• E.g., Skype
clientssupernodes
bootstrapsuper nodecall
relay

TCP Through NATs
• Server socket doesn’t initiate trafﬁc: NAT can’t set
up mapping
• Rendezvous servers (as in Skype)
• Connection reversal through rendezvous if only
one is behind a NAT (rendezvous server asks
un-NAT node to open a port so NAT node can
connect)

TCP Reversal

More NAT Problems
• Port mapping: 0-1023 should map to 0-1023
• Port parity: even port → even port, odd port → odd
port (RFC 3550: RTP uses even, RTCP uses odd))
• Hairpinning: packet from inside NAT can send
packets to external (NAT) address and have
portmap work

RFC 4787 and Hairpinning
• “NAT UDP Unicast Requirements”
- F. Audet and C. Jennings (guest lecture last year)
More formally, a NAT that supports hairpinning forwards packets
originating from an internal address, X1:x1, destined for an external
address X2’:x2’ that has an active mapping to an internal address
X2:x2, back to that internal address, X2:x2. Note that typically X1’
is the same as X2’.
Furthermore, the NAT may present the hairpinned packet with either an
internal (X1:x1) or an external (X1’:x1’) source IP address and port.
Therefore, the hairpinning NAT behavior can be either "External
source IP address and port" or "Internal source IP address and port".
"Internal source IP address and port" may cause problems by confusing
implementations that expect an external IP address and port.

Example confusion
• Two nodes (A, B) share a switch behind a NAT
• A sends TCP SYN to an external address for B
• B responds with SYN+ACK
• What can happen if NAT did not rewrite A’s SYN
to have an external address and port? Will B’s
packet traverse the NAT?

Simple Traversal of UDP through NATs

STUN (RFC 3849)
• “Simple Traversal of User Datagram Protocol
(UDP) Through Network Address Translators
(NATs)”
• Enables a node to
- Determine if it is behind a NAT, and if so, what kind
- Obtain a public IP address/port pair
• Client-server protocol, requires no changes to
NATs
• STUN server coordinates

STUN Binding Requests
• Node sends BR to STUN server
• STUN sends a response that has the address and
port it sees
- If different than node’s local address and port, it’s behind a
NAT
• Node can probe to see what kind of NAT
- Ask STUN server to respond from different address: no
response, address restricted; different response, symmetric
- Ask STUN server to respond from different port: no
response, port restricted
• When does STUN not work?

NAT Hole-Punching
• STUN doesn’t work when
- A or B are behind symmetric NAT
- A and B are behind same NAT without hairpinning
- What about restricted cone, port-restricted NATs?
• Parallel approaches
- A and B report their local IP address to server Sx
- Server tells the other the address/port pair ( L, G )
- A tries to send UDP packets to ( L B , G B ) using L A
- B tries to send UDP packets to ( L A , G A ) using L B

NAT Hole-Punching Example
Client A(10.0.0.101)
NAT(76.18.117.20)
Client B(10.1.1.9)
Server(18.181.0.31)
NAT(128.34.22.8)

NAT Hole-Punching Example
Client A(10.0.0.101)
NAT(76.18.117.20)
Client B(10.1.1.9)
Server(18.181.0.31)
NAT(128.34.22.8)
1. Requestconnection to B

NAT Hole-Punching Example
Client A(10.0.0.101)
Server(18.181.0.31)2a. S sends LBand GB to A2b. S sends LAand GA to B
Client B(10.1.1.9)
NAT(76.18.117.20)NAT(128.34.22.8)

NAT Hole-Punching Example
Client A(10.0.0.101)
Server(18.181.0.31)3a. A sends toLB and GB 3b. B sends toLA and GA
Client B(10.1.1.9)
NAT(76.18.117.20)NAT(128.34.22.8)

NAT Hole-Punching Example
Client A(10.0.0.101)Client B(10.1.1.9)
Server(18.181.0.31)
NAT(76.18.117.20)NAT(128.34.22.8)
4. Session A-Bestablished

Multiple NAT Layers
• Common for consumer Internet: ISP has internal
NAT, end user places another NAT
• Requires hairpinning at ISP NAT
Client A(10.0.0.101)
UserNAT(192.168.3.7)
Client B(10.1.1.9)
ISP NAT(18.181.0.31)
User NAT(192.168.4.1)
Internet
ISP Network

The New Hourglass
Layers 5-7
Layers 1-2
TCPIPUDPICMP
