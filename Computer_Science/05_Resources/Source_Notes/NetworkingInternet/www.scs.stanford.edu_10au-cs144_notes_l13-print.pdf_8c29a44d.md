Title: l13-print.pdf
Mapped Topic: Network systems course notes
Source URL: https://www.scs.stanford.edu/10au-cs144/notes/l13-print.pdf
Source Type: university_course_notes
Trust Score: 95
Fetched At: 2026-04-17T06:57:12+00:00
Mapped From CSE.md Section: Part 1 / Part 2.B

# Content

Lecture 13: Coding, Error Detection and
Correction
Errors and Losses
•Physical layers use encoding to protect link layer
from chip errors
•All or nothing: if chip errors exceed layer 1
robustness, you lose the whole packet (bad CRC)
•We can use these techniques at higher layers as
well:erasure coding
-Encoding data of lengthLasksymbols: anynof thek
symbols can regenerate the original data (n≥L).
Cyclic Redundancy Check (CRC), revisited
•Distillnbits of data into acbit CRC,c< <n
•Can’t detect all errors (2−cchance another packet’s
CRC matches)
•CRCs are designed to detect certain forms of errors
more than others
•Stronger than checksums; detect
-A message with any 1 or 2 bits in error
-A message with any odd number of errors
-A message with an error burst as wide as the CRC
Message Authenticaion Codes
•When sending packets securely (conﬁdentially),
sometimes you use a Message Authentication
Code (MAC) instead of a CRC
•Kind of like a CRC, but seeded with a secret
•MAC needs different properties to be strong
against attackers
-If any bit in the message changes, each bit in the MAC
needs to have an equal probability of being 0 or 1
-Starting with packetP, can’t append data and generate
new MAC
-Can ﬂip a bit and get the same MAC value
Cyclic Redundancy Check, continued
•Can be computed iteratively (e.g., as a packet is
spooled out)
•Mathematical basis
-CRC of lengthncomputed as annth degree polynomial
-CRC of lengthnis remainder after dividing message by a
numberk>2n
-k= 25,k= 11001,x4+x3+x0
•T o detect burst errors of lengthb,n>b
Fields
•A set of numbers of which you can add, subtract,
multiply, and divide
•A ﬁeld can be ﬁnite (Galois Field)
•E.g., Galois FieldGF(p)ﬁeld of integers modulop,
pis prime
•InGF(7),6+3=2

Reed-Solomon
•Standard erasure coding technique: used in CDs
•Core idea: anykdistinct data points deﬁne a
unique polynomial of degreek−1
•Data to transmit deﬁnes the polynomialP
•Compute coded dataC=P(x)forx0,x1,xn
•T ransmitC
•A receiver that getskdifferentxnvalues can
reconstitute original polynomial (and data)
Power of Erasure Coding
•Make datak−1term polynomial
•Computendata points, wheren>k
•Anykdata points can successfully regenerate data
•Can toleraten−klosses, orn−k
2 errors
•Known errors/losses are called erasures: erasure
coding
Code Word Sizes
•Large polynomials lead to large values:63·1910!
•Reed-Solomon works on ﬁelds
•GF(256),63·1910=1 0 6
•Reed-Solomon uses GF(256);
•Sends 223 data symbols, 32 symbols are parity
values (223,255)
•8 bits can have very efﬁcient implementations
Error Burstiness
•Reed-Solomon divides data into code symbols
(e.g., 8 bits)
•Any one bit error invalidates that symbol
•Robust to bursts of errors, weaker against random
errors
•Big bursts can overwhelm the code: CDs use
Cross-Interleaved Reed-Solomon Coding (CIRC)
to spread errors across symbol blocks
Reed-Solomon
•Useful for making media more resilient: operates
on small datum
•Increasing the coding factorkincreases
robustness: can be made robust to arbitrary losses
•Is there some way to do something similar on large
data (e.g., packets?)
Erasure Codes, Revisited
•Data of lengthk
•Erasure codes can regenerate data from any
k(1 +γ)code symbols
•Do not necessarily handle errors
•Perfect world,γ=0(not possible in practice)
•Also want decoding to be fast/simple

Problem Statement
•Have a large piece of data
•Want to deliver it to many client nodes
•Do not want to maintain per-client state
•Goal: send packets, anykpackets can reconsitute
data with very high probability
•Example: television over IP
Why Not Reed-Solomon
•We’re operating on a very large piece of data
•Can deal with larger chunks than Reed-Solomon
•Allows us to do something simpler?
LT Codes
•Data of lengthN
•Code words of lengthl, anylwill do!
•Break data intok=⌈D
L⌉chunksC
•Each transmitted packetCiis an XOR of some
number of random chunks
•Symbol generation isO(ln(k/δ))on average
•Requiresk+O(
√
kln2(k/δ))symbols to decode
with probability1−δ
Power of XOR
•Data A, B, C, D
•Havex0=A, x1=A⊕B, x2=A⊕C, x3=C⊕D
•A=x0
•B=A⊕x1
•C=A⊕x2
•D=C⊕x3
XOR, Visually How to XOR?
•How LT codes XOR the data into code words is
critical
•d(Ci)is the degree of codewordi: how many data
items are XORed in it
•Example bad distributions
-∀Ci,d(Ci)=1: sending data in the clear
-∀Ci,d(Ci)=k−1: each codeword is the XOR of all but one
data symbol
-Both havekunique code words, and require receiving allk

Codeword Degree
LT Decoding Algorithm
•We receivencodewords
•Initially, all input symbols areuncovered
•Each codeword withd=1coversthe input symbol
•Ripple: set of covered input symbols that have not
been processed
•For each symbol in the ripple
-Scan across the codewords and remove it from those that
have it (via XOR), reducing degree by 1
-If codeword has degree 1, cover its input symbol
LT Decoding
•Decoding stops when the ripple is size 0
-If all input symbols are covered, success
-If any input sybmols are uncovered, failure
•How big should the ripple be?
-Small, so there is low redundancy in coverage
-Never zero, because that halts decoding
•Control ripple size through degree distributionρ
2-minute break
LT Encoding
•Two goals
-Minimize number of needed encoding symbols (bps)
-Minimize average degree of encoding symbols (CPU cycles)
•Step through three examples:
-All-at-once:ρ(1) = 1
-Ideal:ρ(1) = 1/k, ρ(i)=1/i(i−1)
-Robust: more on this later
All-at-once
•How many encoded symbols does it take?
•Bins and balls: how many balls must be thrown to
ensure that there is one in each ofkbins?
•O(k·ln(k/δ))for probability1−δ
•Requiresln(k/δ)factor (on averageln(k))
•k=1 0 0 0,δ=0.01%,ln(107)=1 6

Ideal distribution
•ρ(1) = 1/k,∀i, i=2,...,k ,ρ(i)=1/i(i−1)
•Expected behavior is perfect: one input has adof
1, each cover releases another symbol
•Requiresksymbols, sum of degrees isk·ln(k)
•Same sum of degrees as all-at-once, but onlyk
symbols
The World Is Not Ideal
•“However, this heuristic analysis makes the
completely unrealistic assumption that the
expected behavior is the actual behavior, and this
is far from the truth. In fact, the Ideal Soliton
distribution works very poorly in practice because
he expected size of the ripple is one, and even the
smallest variance causes the ripple to vanish and
thus the overall process fails to cover and process
all input symbols.” (Luby)
Robust Distribution
•Size of ripple behaves like a random walk
•Goal: make median point of random walk large
enough to survive variations (ln(k/δ)
√
k)
•Deﬁne a constantR,R=c·ln(k/δ)
√
k
τ(i)=



R/ik i =1, . . . , k/R−1
Rln(R/δ)/k i=k/R
0 i=l/R+1,...,k
•Addτtoρof Ideal, normalize
Improvements of Robust Distribution
•τskews Ideal towards smaller degrees
•Requiresk+O(
√
k·ln2(kδ))(additive factor!)
•k=1 0 0 0,δ=0.01%, requires an extra 88 symbols,
8% overhead.
•Average degree is stillln(k/δ)
Implications
•Example: server wants to deliver 1MB image (1000
1kB packets)
•Server generates packets from robust distribution
•No matter the properties of the lossy channel
(burstiness, periodicity, etc.), there is a 99.99%
chance that a client will be able to regenerate the
image after 1088 packets
•Uses onlyln(k/δ)(e.g., 16) XOR operations per
packet
•Hence the name, “Fountain Code”
MORE
•Chachulski et al., SIGCOMM 2007.
•“MAC-independent Opportunistic Routing &
Encoding”
•Uses network coding in wireless networks to
improve throughput
•Works with unicast ﬂows as well as multicast!
•Sachin Katti, starting in EE/CS in January,
co-authored

Motivation
Unicast
F i g u r e 1 — U n i c a s t E x a m p l e . T h e s o u r c e s e n d s 2 p a c k e t s . T h e d e s t i n a t i o n
o v e r h e a r s p
1
, w h i l e R r e c e i v e s b o t h . R n e e d s t o f o r w a r d j u s t o n e p a c k e t b u t ,
w i t h o u t n o d e - c o o r d i n a t i o n , i t m a y f o r w a r d p
1
, w h i c h i s a l r e a d y k n o w n t o
t h e d e s t i n a t i o n . W i t h n e t w o r k c o d i n g , h o w e v e r , R d o e s n o t n e e d t o k n o w
w h i c h p a c k e t t h e d e s t i n a t i o n m i s s e s . R j u s t s e n d s t h e s u m o f t h e 2 p a c k e t s
p
1
p
2
. T h i s c o d e d p a c k e t a l l o w s t h e d e s t i n a t i o n t o r e t r i e v e t h e p a c k e t i t
m i s s e s i n d e p e n d e n t l y o f i t s i d e n t i t y . O n c e t h e d e s t i n a t i o n r e c e i v e s t h e w h o l e
t r a n s f e r ( p
1
a n d p
2
) , i t a c k s t h e t r a n s f e r c a u s i n g R t o s t o p t r a n s m i t t i n g .
r o u t i n g a n d M A C l a y e r s . M O R E i s M A C - i n d e p e n d e n t , a n d t h u s
c a n e n j o y t h e b a s i c f e a t u r e s a v a i l a b l e t o t o d a y ’ s M A C . S p e c i ﬁ -
c a l l y , i t a c h i e v e s b e t t e r u n i c a s t t h r o u g h p u t b y e x p l o i t i n g t h e s p a -
t i a l r e u s e a v a i l a b l e w i t h 8 0 2 . 1 1 . F u r t h e r , t h e c l e a n s e p a r a t i o n b e -
t w e e n t h e l a y e r s m a k e s M O R E e a s i l y e x t e n s i b l e t o m u l t i c a s t t r a f -
ﬁ c .
O n t h e o t h e r h a n d , M O R E p r e s e n t s a l o w - c o m p l e x i t y d i s t r i b u t e d
a n d 8 0 2 . 1 1 - c o m p a t i b l e a l g o r i t h m f o r i n t r a - ﬂ o w n e t w o r k c o d i n g
o v e r w i r e l e s s u n i c a s t ﬂ o w s . P r i o r w o r k r e q u i r e s s o l v i n g a c o n -
v e x o p t i m i z a t i o n w i t h c o n s t r a i n t s t h a t g r o w e x p o n e n t i a l l y w i t h
t h e m a x i m u m n u m b e r o f n o d e s r e a c h e d b y a b r o a d c a s t [ 2 7 , 2 8 ] .
M O R E a l s o p r e s e n t s t h e ﬁ r s t i m p l e m e n t a t i o n o f w i r e l e s s i n t r a -
ﬂ o w n e t w o r k c o d i n g , d e m o n s t r a t i n g t h e p r a c t i c a l b e n e ﬁ t s o f m i x -
i n g p a c k e t s w i t h i n a w i r e l e s s ﬂ o w .
1
2 . M O T I V A T I N G E X A M P L E S
M O R E ’ s d e s i g n b u i l d s o n t h e t h e o r y o f n e t w o r k c o d i n g [ 2 , 2 6 ,
1 5 ] . I n t h i s s e c t i o n , w e u s e t w o t o y e x a m p l e s t o e x p l a i n t h e i n t u i t i o n
u n d e r l y i n g o u r a p p r o a c h a n d i l l u s t r a t e t h e s y n e r g y b e t w e e n o p p o r -
t u n i s t i c r o u t i n g a n d n e t w o r k c o d i n g .
T h e U n i c a s t C a s e : C o n s i d e r t h e s c e n a r i o i n F i g . 1 . T r a d i t i o n a l r o u t -
i n g p r e d e t e r m i n e s t h e p a t h b e f o r e t r a n s m i s s i o n . I t s e n d s t r a f ﬁ c a l o n g
t h e p a t h “ s r c R d e s t ” , w h i c h h a s t h e h i g h e s t d e l i v e r y p r o b a b i l i t y .
H o w e v e r , w i r e l e s s i s a b r o a d c a s t m e d i u m . W h e n a n o d e t r a n s m i t s ,
t h e r e i s a l w a y s a c h a n c e t h a t a n o d e c l o s e r t h a n t h e c h o s e n n e x t -
h o p t o t h e d e s t i n a t i o n o v e r h e a r s t h e p a c k e t . F o r e x a m p l e , a s s u m e
t h e s o u r c e s e n d s 2 p a c k e t s , p
1
a n d p
2
. T h e n e x t h o p , R , r e c e i v e s b o t h ,
a n d t h e d e s t i n a t i o n h a p p e n s t o o v e r h e a r p
1
. I t w o u l d b e a w a s t e t o
h a v e n o d e R f o r w a r d p
1
a g a i n t o t h e d e s t i n a t i o n . T h i s o b s e r v a t i o n
h a s b e e n n o t e d i n [ 7 ] a n d u s e d t o d e v e l o p E x O R , a n o p p o r t u n i s t i c
r o u t i n g p r o t o c o l f o r m e s h w i r e l e s s n e t w o r k s .
E x O R , h o w e v e r , r e q u i r e s n o d e c o o r d i n a t i o n , w h i c h i s m o r e d i f ﬁ -
c u l t i n l a r g e r n e t w o r k s . C o n s i d e r a g a i n t h e e x a m p l e i n t h e p r e v i o u s
p a r a g r a p h . R s h o u l d f o r w a r d o n l y p a c k e t p
2
b e c a u s e t h e ﬁ r s t p a c k e t
h a s a l r e a d y b e e n r e c e i v e d b y t h e d e s t i n a t i o n ; b u t , w i t h o u t c o n s u l t i n g
w i t h t h e d e s t i n a t i o n , R h a s n o w a y o f k n o w i n g w h i c h p a c k e t t o t r a n s -
m i t . T h e p r o b l e m b e c o m e s h a r d e r i n l a r g e r n e t w o r k s , w h e r e m a n y
n o d e s h e a r a t r a n s m i t t e d p a c k e t . O p p o r t u n i s t i c r o u t i n g a l l o w s t h e s e
n o d e s t o p a r t i c i p a t e i n f o r w a r d i n g t h e h e a r d p a c k e t s . W i t h o u t c o -
o r d i n a t i o n , h o w e v e r , m u l t i p l e n o d e s m a y u n n e c e s s a r i l y f o r w a r d t h e
s a m e p a c k e t s , c r e a t i n g s p u r i o u s t r a n s m i s s i o n s . T o d e a l w i t h t h i s i s -
s u e , E x O R i m p o s e s a s p e c i a l s c h e d u l e r o n t o p o f 8 0 2 . 1 1 . T h e s c h e d -
u l e r g o e s i n r o u n d s a n d r e s e r v e s t h e m e d i u m f o r a s i n g l e f o r w a r d e r
1
I n c o n t r a s t , C O P E [ 2 3 ] i s t h e ﬁ r s t i m p l e m e n t a t i o n t h a t d e m o n -
s t r a t e s p r a c t i c a l b e n e ﬁ t s f o r i n t e r - ﬂ o w w i r e l e s s n e t w o r k c o d i n g .
F i g u r e 2 — M u l t i c a s t E x a m p l e . I n s t e a d o f r e t r a n s m i t t i n g a l l f o u r p a c k e t s ,
t h e s o u r c e c a n t r a n s m i t t w o l i n e a r c o m b i n a t i o n s , e . g . , p
1
p
2
p
3
p
4
a n d
p
1
2 p
2
3 p
3
4 p
4
. T h e s e t w o c o d e d p a c k e t s a l l o w a l l t h r e e d e s t i n a t i o n s
t o r e t r i e v e t h e f o u r o r i g i n a l p a c k e t s , s a v i n g t h e s o u r c e 2 t r a n s m i s s i o n s .
a t a n y o n e t i m e . T h e r e s t o f t h e n o d e s l i s t e n t o l e a r n t h e p a c k e t s o v e r -
h e a r d b y e a c h n o d e . D u e t o t h i s s t r i c t s c h e d u l e , n o d e s f a r t h e r a w a y
f r o m t h e d e s t i n a t i o n ( w h i c h c o u l d p o t e n t i a l l y h a v e t r a n s m i t t e d a t t h e
s a m e t i m e a s n o d e s c l o s e t o t h e d e s t i n a t i o n d u e t o s p a t i a l r e u s e ) ,
c a n n o t , s i n c e t h e y h a v e t o w a i t f o r t h e n o d e s c l o s e t o t h e d e s t i n a -
t i o n t o ﬁ n i s h t r a n s m i t t i n g . H e n c e t h e s c h e d u l e r h a s t h e s i d e e f f e c t o f
p r e v e n t i n g a ﬂ o w f r o m e x p l o i t i n g s p a t i a l r e u s e .
N e t w o r k c o d i n g o f f e r s a n e l e g a n t s o l u t i o n t o t h e a b o v e p r o b l e m .
I n o u r e x a m p l e , t h e d e s t i n a t i o n h a s o v e r h e a r d o n e o f t h e t r a n s m i t -
t e d p a c k e t s , p
1
, b u t n o d e R i s u n a w a r e o f t h i s f o r t u n a t e r e c e p t i o n .
W i t h n e t w o r k c o d i n g , n o d e R n a t u r a l l y f o r w a r d s l i n e a r c o m b i n a t i o n s
o f t h e r e c e i v e d p a c k e t s . F o r e x a m p l e , R c a n s e n d t h e s u m p
1
p
2
.
T h e d e s t i n a t i o n r e t r i e v e s t h e p a c k e t p
2
i t m i s s e s b y s u b t r a c t i n g f r o m
t h e s u m a n d a c k s t h e w h o l e t r a n s f e r . T h u s , R n e e d n o t k n o w w h i c h
p a c k e t t h e d e s t i n a t i o n h a s o v e r h e a r d .
I n d e e d , t h e a b o v e w o r k s i f R s e n d s a n y r a n d o m l i n e a r c o m b i n a t i o n
o f t h e t w o p a c k e t s i n s t e a d o f t h e s u m . T h u s , o n e c a n g e n e r a l i z e t h e
a b o v e a p p r o a c h . T h e s o u r c e b r o a d c a s t s i t s p a c k e t s . R o u t e r s c r e a t e
r a n d o m l i n e a r c o m b i n a t i o n s o f t h e p a c k e t s t h e y h e a r ( i . e . , c
1
p
1
c
n
p
n
, w h e r e c
i
i s a r a n d o m c o e f ﬁ c i e n t ) . T h e d e s t i n a t i o n s e n d s
a n a c k a l o n g t h e r e v e r s e p a t h o n c e i t r e c e i v e s t h e w h o l e t r a n s f e r . T h i s
a p p r o a c h d o e s n o t r e q u i r e n o d e c o o r d i n a t i o n a n d p r e s e r v e s s p a t i a l
r e u s e .
T h e M u l t i c a s t C a s e : O u r s e c o n d e x a m p l e i l l u s t r a t e s t h e s y n e r g y
b e t w e e n n e t w o r k c o d i n g a n d m u l t i c a s t . I n F i g . 2 , t h e s o u r c e m u l t i -
c a s t s 4 p a c k e t s t o t h r e e d e s t i n a t i o n s . W i r e l e s s r e c e p t i o n s a t d i f f e r e n t
n o d e s a r e k n o w n t o b e h i g h l y i n d e p e n d e n t [ 3 2 , 3 0 ] . A s s u m e t h a t
e a c h d e s t i n a t i o n r e c e i v e s t h e p a c k e t s i n d i c a t e d i n t h e ﬁ g u r e – i . e . , t h e
ﬁ r s t d e s t i n a t i o n r e c e i v e s p
1
a n d p
2
, t h e s e c o n d d e s t i n a t i o n r e c e i v e s
p
2
a n d p
3
, a n d t h e l a s t d e s t i n a t i o n r e c e i v e s p
3
a n d p
4
. N o t e t h a t e a c h
o f t h e f o u r p a c k e t s i s l o s t b y s o m e d e s t i n a t i o n .
W i t h o u t c o d i n g , t h e s e n d e r h a s t o r e t r a n s m i t t h e u n i o n o f a l l
l o s t p a c k e t s , i . e . , t h e s e n d e r n e e d s t o r e t r a n s m i t a l l f o u r p a c k e t s .
I n c o n t r a s t , w i t h n e t w o r k c o d i n g , i t i s s u f ﬁ c i e n t t o t r a n s m i t 2 r a n -
d o m l y c o d e d p a c k e t s . F o r e x a m p l e , t h e s e n d e r m a y s e n d p
1
p
1
p
2
p
3
p
4
a n d p
2
p
1
2 p
2
3 p
3
4 p
4
. D e s p i t e t h e f a c t
t h a t t h e y l o s t d i f f e r e n t p a c k e t s , a l l t h r e e d e s t i n a t i o n s c a n r e t r i e v e t h e
f o u r o r i g i n a l p a c k e t s u s i n g t h e s e t w o c o d e d p a c k e t s . F o r e x a m p l e ,
t h e ﬁ r s t d e s t i n a t i o n , w h i c h h a s r e c e i v e d p
1
, p
2
a n d p
1
, p
2
, r e t r i e v e s
a l l f o u r o r i g i n a l p a c k e t s b y i n v e r t i n g t h e m a t r i x o f c o e f ﬁ c i e n t s , a n d
m u l t i p l y i n g i t w i t h t h e p a c k e t s i t r e c e i v e d , a s f o l l o w s :
p
1
p
2
p
3
p
4
1 1 1 1
1 2 3 4
1 0 0 0
0 1 0 0
1
p
1
p
2
p
1
p
2
.
T h u s , i n t h i s s i m p l e e x a m p l e , n e t w o r k c o d i n g h a s r e d u c e d t h e
n e e d e d r e t r a n s m i s s i o n s f r o m 4 p a c k e t s t o 2 , i m p r o v i n g t h e o v e r a l l
t h r o u g h p u t .
Multicast
F i g u r e 1 — U n i c a s t E x a m p l e . T h e s o u r c e s e n d s 2 p a c k e t s . T h e d e s t i n a t i o n
o v e r h e a r s p
1
, w h i l e R r e c e i v e s b o t h . R n e e d s t o f o r w a r d j u s t o n e p a c k e t b u t ,
w i t h o u t n o d e - c o o r d i n a t i o n , i t m a y f o r w a r d p
1
, w h i c h i s a l r e a d y k n o w n t o
t h e d e s t i n a t i o n . W i t h n e t w o r k c o d i n g , h o w e v e r , R d o e s n o t n e e d t o k n o w
w h i c h p a c k e t t h e d e s t i n a t i o n m i s s e s . R j u s t s e n d s t h e s u m o f t h e 2 p a c k e t s
p
1
p
2
. T h i s c o d e d p a c k e t a l l o w s t h e d e s t i n a t i o n t o r e t r i e v e t h e p a c k e t i t
m i s s e s i n d e p e n d e n t l y o f i t s i d e n t i t y . O n c e t h e d e s t i n a t i o n r e c e i v e s t h e w h o l e
t r a n s f e r ( p
1
a n d p
2
) , i t a c k s t h e t r a n s f e r c a u s i n g R t o s t o p t r a n s m i t t i n g .
r o u t i n g a n d M A C l a y e r s . M O R E i s M A C - i n d e p e n d e n t , a n d t h u s
c a n e n j o y t h e b a s i c f e a t u r e s a v a i l a b l e t o t o d a y ’ s M A C . S p e c i ﬁ -
c a l l y , i t a c h i e v e s b e t t e r u n i c a s t t h r o u g h p u t b y e x p l o i t i n g t h e s p a -
t i a l r e u s e a v a i l a b l e w i t h 8 0 2 . 1 1 . F u r t h e r , t h e c l e a n s e p a r a t i o n b e -
t w e e n t h e l a y e r s m a k e s M O R E e a s i l y e x t e n s i b l e t o m u l t i c a s t t r a f -
ﬁ c .
O n t h e o t h e r h a n d , M O R E p r e s e n t s a l o w - c o m p l e x i t y d i s t r i b u t e d
a n d 8 0 2 . 1 1 - c o m p a t i b l e a l g o r i t h m f o r i n t r a - ﬂ o w n e t w o r k c o d i n g
o v e r w i r e l e s s u n i c a s t ﬂ o w s . P r i o r w o r k r e q u i r e s s o l v i n g a c o n -
v e x o p t i m i z a t i o n w i t h c o n s t r a i n t s t h a t g r o w e x p o n e n t i a l l y w i t h
t h e m a x i m u m n u m b e r o f n o d e s r e a c h e d b y a b r o a d c a s t [ 2 7 , 2 8 ] .
M O R E a l s o p r e s e n t s t h e ﬁ r s t i m p l e m e n t a t i o n o f w i r e l e s s i n t r a -
ﬂ o w n e t w o r k c o d i n g , d e m o n s t r a t i n g t h e p r a c t i c a l b e n e ﬁ t s o f m i x -
i n g p a c k e t s w i t h i n a w i r e l e s s ﬂ o w .
1
2 . M O T I V A T I N G E X A M P L E S
M O R E ’ s d e s i g n b u i l d s o n t h e t h e o r y o f n e t w o r k c o d i n g [ 2 , 2 6 ,
1 5 ] . I n t h i s s e c t i o n , w e u s e t w o t o y e x a m p l e s t o e x p l a i n t h e i n t u i t i o n
u n d e r l y i n g o u r a p p r o a c h a n d i l l u s t r a t e t h e s y n e r g y b e t w e e n o p p o r -
t u n i s t i c r o u t i n g a n d n e t w o r k c o d i n g .
T h e U n i c a s t C a s e : C o n s i d e r t h e s c e n a r i o i n F i g . 1 . T r a d i t i o n a l r o u t -
i n g p r e d e t e r m i n e s t h e p a t h b e f o r e t r a n s m i s s i o n . I t s e n d s t r a f ﬁ c a l o n g
t h e p a t h “ s r c R d e s t ” , w h i c h h a s t h e h i g h e s t d e l i v e r y p r o b a b i l i t y .
H o w e v e r , w i r e l e s s i s a b r o a d c a s t m e d i u m . W h e n a n o d e t r a n s m i t s ,
t h e r e i s a l w a y s a c h a n c e t h a t a n o d e c l o s e r t h a n t h e c h o s e n n e x t -
h o p t o t h e d e s t i n a t i o n o v e r h e a r s t h e p a c k e t . F o r e x a m p l e , a s s u m e
t h e s o u r c e s e n d s 2 p a c k e t s , p
1
a n d p
2
. T h e n e x t h o p , R , r e c e i v e s b o t h ,
a n d t h e d e s t i n a t i o n h a p p e n s t o o v e r h e a r p
1
. I t w o u l d b e a w a s t e t o
h a v e n o d e R f o r w a r d p
1
a g a i n t o t h e d e s t i n a t i o n . T h i s o b s e r v a t i o n
h a s b e e n n o t e d i n [ 7 ] a n d u s e d t o d e v e l o p E x O R , a n o p p o r t u n i s t i c
r o u t i n g p r o t o c o l f o r m e s h w i r e l e s s n e t w o r k s .
E x O R , h o w e v e r , r e q u i r e s n o d e c o o r d i n a t i o n , w h i c h i s m o r e d i f ﬁ -
c u l t i n l a r g e r n e t w o r k s . C o n s i d e r a g a i n t h e e x a m p l e i n t h e p r e v i o u s
p a r a g r a p h . R s h o u l d f o r w a r d o n l y p a c k e t p
2
b e c a u s e t h e ﬁ r s t p a c k e t
h a s a l r e a d y b e e n r e c e i v e d b y t h e d e s t i n a t i o n ; b u t , w i t h o u t c o n s u l t i n g
w i t h t h e d e s t i n a t i o n , R h a s n o w a y o f k n o w i n g w h i c h p a c k e t t o t r a n s -
m i t . T h e p r o b l e m b e c o m e s h a r d e r i n l a r g e r n e t w o r k s , w h e r e m a n y
n o d e s h e a r a t r a n s m i t t e d p a c k e t . O p p o r t u n i s t i c r o u t i n g a l l o w s t h e s e
n o d e s t o p a r t i c i p a t e i n f o r w a r d i n g t h e h e a r d p a c k e t s . W i t h o u t c o -
o r d i n a t i o n , h o w e v e r , m u l t i p l e n o d e s m a y u n n e c e s s a r i l y f o r w a r d t h e
s a m e p a c k e t s , c r e a t i n g s p u r i o u s t r a n s m i s s i o n s . T o d e a l w i t h t h i s i s -
s u e , E x O R i m p o s e s a s p e c i a l s c h e d u l e r o n t o p o f 8 0 2 . 1 1 . T h e s c h e d -
u l e r g o e s i n r o u n d s a n d r e s e r v e s t h e m e d i u m f o r a s i n g l e f o r w a r d e r
1
I n c o n t r a s t , C O P E [ 2 3 ] i s t h e ﬁ r s t i m p l e m e n t a t i o n t h a t d e m o n -
s t r a t e s p r a c t i c a l b e n e ﬁ t s f o r i n t e r - ﬂ o w w i r e l e s s n e t w o r k c o d i n g .
F i g u r e 2 — M u l t i c a s t E x a m p l e . I n s t e a d o f r e t r a n s m i t t i n g a l l f o u r p a c k e t s ,
t h e s o u r c e c a n t r a n s m i t t w o l i n e a r c o m b i n a t i o n s , e . g . , p
1
p
2
p
3
p
4
a n d
p
1
2 p
2
3 p
3
4 p
4
. T h e s e t w o c o d e d p a c k e t s a l l o w a l l t h r e e d e s t i n a t i o n s
t o r e t r i e v e t h e f o u r o r i g i n a l p a c k e t s , s a v i n g t h e s o u r c e 2 t r a n s m i s s i o n s .
a t a n y o n e t i m e . T h e r e s t o f t h e n o d e s l i s t e n t o l e a r n t h e p a c k e t s o v e r -
h e a r d b y e a c h n o d e . D u e t o t h i s s t r i c t s c h e d u l e , n o d e s f a r t h e r a w a y
f r o m t h e d e s t i n a t i o n ( w h i c h c o u l d p o t e n t i a l l y h a v e t r a n s m i t t e d a t t h e
s a m e t i m e a s n o d e s c l o s e t o t h e d e s t i n a t i o n d u e t o s p a t i a l r e u s e ) ,
c a n n o t , s i n c e t h e y h a v e t o w a i t f o r t h e n o d e s c l o s e t o t h e d e s t i n a -
t i o n t o ﬁ n i s h t r a n s m i t t i n g . H e n c e t h e s c h e d u l e r h a s t h e s i d e e f f e c t o f
p r e v e n t i n g a ﬂ o w f r o m e x p l o i t i n g s p a t i a l r e u s e .
N e t w o r k c o d i n g o f f e r s a n e l e g a n t s o l u t i o n t o t h e a b o v e p r o b l e m .
I n o u r e x a m p l e , t h e d e s t i n a t i o n h a s o v e r h e a r d o n e o f t h e t r a n s m i t -
t e d p a c k e t s , p
1
, b u t n o d e R i s u n a w a r e o f t h i s f o r t u n a t e r e c e p t i o n .
W i t h n e t w o r k c o d i n g , n o d e R n a t u r a l l y f o r w a r d s l i n e a r c o m b i n a t i o n s
o f t h e r e c e i v e d p a c k e t s . F o r e x a m p l e , R c a n s e n d t h e s u m p
1
p
2
.
T h e d e s t i n a t i o n r e t r i e v e s t h e p a c k e t p
2
i t m i s s e s b y s u b t r a c t i n g f r o m
t h e s u m a n d a c k s t h e w h o l e t r a n s f e r . T h u s , R n e e d n o t k n o w w h i c h
p a c k e t t h e d e s t i n a t i o n h a s o v e r h e a r d .
I n d e e d , t h e a b o v e w o r k s i f R s e n d s a n y r a n d o m l i n e a r c o m b i n a t i o n
o f t h e t w o p a c k e t s i n s t e a d o f t h e s u m . T h u s , o n e c a n g e n e r a l i z e t h e
a b o v e a p p r o a c h . T h e s o u r c e b r o a d c a s t s i t s p a c k e t s . R o u t e r s c r e a t e
r a n d o m l i n e a r c o m b i n a t i o n s o f t h e p a c k e t s t h e y h e a r ( i . e . , c
1
p
1
c
n
p
n
, w h e r e c
i
i s a r a n d o m c o e f ﬁ c i e n t ) . T h e d e s t i n a t i o n s e n d s
a n a c k a l o n g t h e r e v e r s e p a t h o n c e i t r e c e i v e s t h e w h o l e t r a n s f e r . T h i s
a p p r o a c h d o e s n o t r e q u i r e n o d e c o o r d i n a t i o n a n d p r e s e r v e s s p a t i a l
r e u s e .
T h e M u l t i c a s t C a s e : O u r s e c o n d e x a m p l e i l l u s t r a t e s t h e s y n e r g y
b e t w e e n n e t w o r k c o d i n g a n d m u l t i c a s t . I n F i g . 2 , t h e s o u r c e m u l t i -
c a s t s 4 p a c k e t s t o t h r e e d e s t i n a t i o n s . W i r e l e s s r e c e p t i o n s a t d i f f e r e n t
n o d e s a r e k n o w n t o b e h i g h l y i n d e p e n d e n t [ 3 2 , 3 0 ] . A s s u m e t h a t
e a c h d e s t i n a t i o n r e c e i v e s t h e p a c k e t s i n d i c a t e d i n t h e ﬁ g u r e – i . e . , t h e
ﬁ r s t d e s t i n a t i o n r e c e i v e s p
1
a n d p
2
, t h e s e c o n d d e s t i n a t i o n r e c e i v e s
p
2
a n d p
3
, a n d t h e l a s t d e s t i n a t i o n r e c e i v e s p
3
a n d p
4
. N o t e t h a t e a c h
o f t h e f o u r p a c k e t s i s l o s t b y s o m e d e s t i n a t i o n .
W i t h o u t c o d i n g , t h e s e n d e r h a s t o r e t r a n s m i t t h e u n i o n o f a l l
l o s t p a c k e t s , i . e . , t h e s e n d e r n e e d s t o r e t r a n s m i t a l l f o u r p a c k e t s .
I n c o n t r a s t , w i t h n e t w o r k c o d i n g , i t i s s u f ﬁ c i e n t t o t r a n s m i t 2 r a n -
d o m l y c o d e d p a c k e t s . F o r e x a m p l e , t h e s e n d e r m a y s e n d p
1
p
1
p
2
p
3
p
4
a n d p
2
p
1
2 p
2
3 p
3
4 p
4
. D e s p i t e t h e f a c t
t h a t t h e y l o s t d i f f e r e n t p a c k e t s , a l l t h r e e d e s t i n a t i o n s c a n r e t r i e v e t h e
f o u r o r i g i n a l p a c k e t s u s i n g t h e s e t w o c o d e d p a c k e t s . F o r e x a m p l e ,
t h e ﬁ r s t d e s t i n a t i o n , w h i c h h a s r e c e i v e d p
1
, p
2
a n d p
1
, p
2
, r e t r i e v e s
a l l f o u r o r i g i n a l p a c k e t s b y i n v e r t i n g t h e m a t r i x o f c o e f ﬁ c i e n t s , a n d
m u l t i p l y i n g i t w i t h t h e p a c k e t s i t r e c e i v e d , a s f o l l o w s :
p
1
p
2
p
3
p
4
1 1 1 1
1 2 3 4
1 0 0 0
0 1 0 0
1
p
1
p
2
p
1
p
2
.
T h u s , i n t h i s s i m p l e e x a m p l e , n e t w o r k c o d i n g h a s r e d u c e d t h e
n e e d e d r e t r a n s m i s s i o n s f r o m 4 p a c k e t s t o 2 , i m p r o v i n g t h e o v e r a l l
t h r o u g h p u t .
MORE at Layer 2.5
MORE at Layer 2.5
MORE Summary
•A coded packet is a linear combination of native
packets
•MORE adds a header that contains the linear
coefﬁcients
•MORE uses opportunistic reception: nodes
broadcast coded packets to some number of next
hops, more than one of which can forward the
packet
•Source collects native packets into a batch, starts
sending linear combinations of those packets,
stops when it receives an end-to-end ACK.
Opportunistic Reception
•MORE maintains ETX-based route estimates
•MORE picksnforwarders which are closer to the
destination than it, ordered according to their
proximity (nclosest)
Forwarding Packets
•Some received coded packets are innovative: they
are linearly independent of prior packets
(bounded by batch sizeK)
•Forwarders discard packets that are not innovative
•Whenever a forwarder receives a packet, it gets a
transmit credit
•Sending a packet costs a credit
•ETX ordering prevents loops and credit explosion

Encoding and Decoding Packets
•Source makes each encoded packet a random
linear combination of native packets
•Forwarders send random linear combinations of
encoded packets (which are still linear
combinations)
•Klinearly independent combinations allow the
destination to decode packet through simple
matrix inversion.
When T o Stop?
•When destination determines it can decode, it
immediately sends an end-to-end ACK (don’t even
wait for decoding)
•Every node that hears the ACK stops
•When the source stops, forwarders stop getting
transmit credits
•ACK packets are put on fast path: take precedence
over all data packets
Improvement
F i g u r e 5 — O n e F l o o r o f o u r T e s t b e d . N o d e s ’ l o c a t i o n o n o n e ﬂ o o r o f o u r
3 - ﬂ o o r t e s t b e d .
a n t e n n a . T h e y t r a n s m i t a t a p o w e r l e v e l o f 1 8 d B m , a n d o p e r a t e i n
t h e 8 0 2 . 1 1 a d h o c m o d e , w i t h R T S / C T S d i s a b l e d .
( c ) S o f t w a r e : N o d e s i n t h e t e s t b e d r u n L i n u x , t h e C l i c k t o o l k i t [ 2 5 ]
a n d t h e R o o f n e t s o f t w a r e p a c k a g e [ 1 ] . O u r i m p l e m e n t a t i o n r u n s a s
a u s e r s p a c e d a e m o n o n L i n u x . I t s e n d s a n d r e c e i v e s r a w 8 0 2 . 1 1
f r a m e s f r o m t h e w i r e l e s s d e v i c e u s i n g a l i b p c a p - l i k e i n t e r f a c e .
8 . 2 C o m p a r e d P r o t o c o l s
W e c o m p a r e t h e f o l l o w i n g t h r e e p r o t o c o l s .
M O R E a s e x p l a i n e d i n 6 .
E x O R [ 7 ] , t h e c u r r e n t o p p o r t u n i s t i c r o u t i n g p r o t o c o l . O u r E x O R
c o d e i s p r o v i d e d b y i t s a u t h o r s .
S r c r [ 6 ] w h i c h i s a s t a t e - o f - t h e - a r t b e s t p a t h r o u t i n g p r o t o c o l f o r
w i r e l e s s m e s h n e t w o r k s . I t u s e s D i j k s t r a ’ s s h o r t e s t p a t h a l g o r i t h m
w h e r e l i n k w e i g h t s a r e a s s i g n e d b a s e d o n t h e E T X m e t r i c [ 1 1 ] .
8 . 3 S e t u p
I n e a c h e x p e r i m e n t , w e r u n S r c r , M O R E , a n d E x O R i n s e q u e n c e
b e t w e e n t h e s a m e s o u r c e d e s t i n a t i o n p a i r s . E a c h r u n t r a n s f e r s a 5
M B y t e ﬁ l e . W e l e v e r a g e t h e E T X i m p l e m e n t a t i o n p r o v i d e d w i t h t h e
R o o f n e t s o f t w a r e t o m e a s u r e l i n k d e l i v e r y p r o b a b i l i t i e s . B e f o r e r u n -
n i n g a n e x p e r i m e n t , w e r u n t h e E T X m e a s u r e m e n t m o d u l e f o r 1 0
m i n u t e s t o c o m p u t e p a i r - w i s e d e l i v e r y p r o b a b i l i t i e s a n d t h e c o r r e -
s p o n d i n g E T X m e t r i c . T h e s e m e a s u r e m e n t s a r e t h e n f e d t o a l l t h r e e
p r o t o c o l s , S r c r , M O R E , a n d E x O R , a n d u s e d f o r r o u t e s e l e c t i o n .
U n l e s s s t a t e d d i f f e r e n t l y , t h e b a t c h s i z e f o r b o t h M O R E a n d E x O R
i s s e t t o K 3 2 p a c k e t s . T h e p a c k e t s i z e f o r a l l t h r e e p r o t o c o l s i s
1 5 0 0 B . T h e q u e u e s i z e a t S r c r r o u t e r s i s 5 0 p a c k e t s . I n c o n t r a s t ,
M O R E a n d E x O R d o n o t u s e q u e u e s ; t h e y b u f f e r a c t i v e b a t c h e s .
M o s t e x p e r i m e n t s a r e p e r f o r m e d o v e r 8 0 2 . 1 1 b w i t h a b i t - r a t e o f
5 . 5 M b / s . I n 8 . 7 , w e a l l o w t r a d i t i o n a l r o u t i n g ( i . e . , S r c r ) t o e x p l o i t
t h e a u t o r a t e f e a t u r e i n t h e M a d W i ﬁ d r i v e r , w h i c h u s e s t h e O n o e
b i t - r a t e s e l e c t i o n a l g o r i t h m [ 5 ] . C u r r e n t a u t o r a t e c o n t r o l o p t i m i z e s
t h e b i t - r a t e f o r t h e n e x t h o p , m a k i n g i t u n s u i t a b l e f o r o p p o r t u n i s t i c
r o u t i n g , w h i c h b r o a d c a s t s e v e r y t r a n s m i s s i o n t o m a n y p o t e n t i a l n e x -
t h o p s . T h e p r o b l e m o f a u t o r a t e c o n t r o l f o r o p p o r t u n i s t i c r o u t i n g i s
s t i l l o p e n . T h u s i n o u r e x p e r i m e n t s , w e c o m p a r e S r c r w i t h a u t o r a t e
t o o p p o r t u n i s t i c r o u t i n g ( M O R E a n d E x O R ) w i t h a ﬁ x e d b i t - r a t e o f
1 1 M b / s .
8 . 4 T h r o u g h p u t
W e w o u l d l i k e t o e x a m i n e w h e t h e r M O R E c a n e f f e c t i v e l y e x p l o i t
o p p o r t u n i s t i c r e c e p t i o n s t o i m p r o v e t h e t h r o u g h p u t a n d c o m p a r e i t
w i t h S r c r a n d E x O R .
0
0 . 1
0 . 2
0 . 3
0 . 4
0 . 5
0 . 6
0 . 7
0 . 8
0 . 9
1
0 5 0 1 0 0 1 5 0 2 0 0
C u m u l a t i v e F r a c t i o n o f F l o w s
T h r o u g h p u t [ p k t / s ]
S r c r
E x O R
M O R E
F i g u r e 6 — U n i c a s t T h r o u g h p u t . F i g u r e s h o w s t h e C D F o f t h e u n i -
c a s t t h r o u g h p u t a c h i e v e d w i t h M O R E , E x O R , a n d S r c r . M O R E ’ s m e d i a n
t h r o u g h p u t i s 2 2 % h i g h e r t h a n E x O R . I n c o m p a r i s o n t o S r c r , M O R E a c h i e v e s
a m e d i a n t h r o u g h p u t g a i n o f 9 5 % , w h i l e s o m e s o u r c e - d e s t i n a t i o n p a i r s s h o w
a s m u c h a s 1 0 - 1 2 x .
( a ) H o w D o t h e T h r e e P r o t o c o l s C o m p a r e ? D o e s M O R E i m p r o v e
o v e r E x O R ? H o w d o t h e s e t w o o p p o r t u n i s t i c r o u t i n g p r o t o c o l s c o m -
p a r e w i t h t r a d i t i o n a l b e s t p a t h r o u t i n g ? T o a n s w e r t h e s e q u e s t i o n s ,
w e u s e t h e s e p r o t o c o l s t o t r a n s f e r a 5 M B y t e ﬁ l e b e t w e e n v a r i o u s
n o d e s i n o u r t e s t b e d . W e r e p e a t t h e s a m e e x p e r i m e n t f o r M O R E ,
E x O R , a n d S r c r a s e x p l a i n e d i n 8 . 3 .
O u r r e s u l t s s h o w t h a t M O R E s i g n i ﬁ c a n t l y i m p r o v e s t h e u n i c a s t
t h r o u g h p u t . I n p a r t i c u l a r , F i g . 6 p l o t s t h e C D F o f t h e t h r o u g h -
p u t t a k e n o v e r 2 0 0 r a n d o m l y s e l e c t e d s o u r c e - d e s t i n a t i o n p a i r s i n
o u r t e s t b e d . T h e ﬁ g u r e s h o w s t h a t b o t h M O R E a n d E x O R s i g n i f -
i c a n t l y o u t p e r f o r m S r c r . I n t e r e s t i n g l y , h o w e v e r , M O R E ’ s t h r o u g h -
p u t i s h i g h e r t h a n E x O R ’ s . I n t h e m e d i a n c a s e , M O R E h a s a 2 2 %
t h r o u g h p u t g a i n o v e r E x O R . I t s t h r o u g h p u t g a i n o v e r S r c r i s 9 5 % ,
b u t s o m e c h a l l e n g e d ﬂ o w s a c h i e v e 1 0 - 1 2 x h i g h e r t h r o u g h p u t w i t h
M O R E t h a n t r a d i t i o n a l r o u t i n g .
F u r t h e r , M O R E a n d o p p o r t u n i s t i c r o u t i n g e a s e t h e p r o b l e m o f
d e a d s p o t s . F i g . 6 s h o w s t h a t o v e r 9 0 % o f M O R E ﬂ o w s h a v e a
t h r o u g h p u t l a r g e r t h a n 5 1 p a c k e t s a s e c o n d . E x O R ’ s 1 0
t h
p e r c e n t i l e
i s a t 3 5 p a c k e t s a s e c o n d . S r c r o n t h e o t h e r h a n d s u f f e r s f r o m d e a d
s p o t s w i t h m a n y ﬂ o w s e x p e r i e n c i n g v e r y l o w t h r o u g h p u t . S p e c i ﬁ -
c a l l y , t h e 1 0
t h
p e r c e n t i l e o f S r c r ’ s t h r o u g h p u t i s a t 1 2 p a c k e t s a s e c -
o n d .
( b ) W h e n D o e s O p p o r t u n i s t i c R o u t i n g W i n ? W e t r y t o i d e n t i f y
t h e s c e n a r i o s i n w h i c h p r o t o c o l s l i k e M O R E a n d E x O R a r e p a r t i c -
u l a r l y u s e f u l , i . e . , w h e n s h o u l d o n e e x p e c t o p p o r t u n i s t i c r o u t i n g t o
b r i n g a l a r g e t h r o u g h p u t g a i n ? F i g . 7 a s h o w s t h e s c a t t e r p l o t f o r t h e
t h r o u g h p u t s a c h i e v e d u n d e r S r c r a n d M O R E f o r t h e s a m e s o u r c e -
d e s t i n a t i o n p a i r . F i g . 7 b g i v e s a n a n a l o g o u s p l o t f o r E x O R . P o i n t s
o n t h e 4 5 - d e g r e e l i n e h a v e t h e s a m e t h r o u g h p u t i n t h e t w o c o m p a r e d
s c h e m e s .
T h e s e ﬁ g u r e s r e v e a l t h a t o p p o r t u n i s t i c r o u t i n g ( M O R E a n d
E x O R ) g r e a t l y i m p r o v e s p e r f o r m a n c e f o r c h a l l e n g e d ﬂ o w s , i . e . ,
ﬂ o w s t h a t u s u a l l y h a v e l o w t h r o u g h p u t . F l o w s t h a t a c h i e v e g o o d
t h r o u g h p u t u n d e r S r c r d o n o t i m p r o v e f u r t h e r . T h i s i s b e c a u s e w h e n
l i n k s o n t h e b e s t p a t h h a v e v e r y g o o d q u a l i t y , t h e r e i s l i t t l e b e n -
e ﬁ t f r o m e x p l o i t i n g o p p o r t u n i s t i c r e c e p t i o n s . I n c o n t r a s t , a s o u r c e -
d e s t i n a t i o n p a i r t h a t o b t a i n s l o w t h r o u g h p u t u n d e r S r c r d o e s n o t h a v e
a n y g o o d q u a l i t y p a t h . U s u a l l y , h o w e v e r , m a n y l o w - q u a l i t y p a t h s e x -
i s t b e t w e e n t h e s o u r c e a n d t h e d e s t i n a t i o n . B y u s i n g t h e c o m b i n e d
c a p a c i t y o f a l l t h e s e l o w - q u a l i t y p a t h s , M O R E a n d E x O R m a n a g e t o
b o o s t t h e t h r o u g h p u t o f s u c h ﬂ o w s .
( c ) W h y D o e s M O R E H a v e H i g h e r T h r o u g h p u t t h a n E x O R ?
O u r e x p e r i m e n t s s h o w t h a t s p a t i a l r e u s e i s a m a i n c o n t r i b u t o r t o
M O R E ’ s g a i n o v e r E x O R . E x O R p r e v e n t s m u l t i p l e f o r w a r d e r s f r o m
a c c e s s i n g t h e m e d i u m s i m u l t a n e o u s l y [ 7 ] , a n d t h u s d o e s n o t e x p l o i t
Long Routes
1
1 0
1 0 0
1 1 0 1 0 0
M O R E T h r o u g h p u t [ p k t / s ]
S r c r T h r o u g h p u t [ p k t / s ]
( a ) M O R E v s . S r c r
1
1 0
1 0 0
1 1 0 1 0 0
E x O R T h r o u g h p u t [ p k t / s ]
S r c r T h r o u g h p u t [ p k t / s ]
( b ) E x O R v s . S r c r
F i g u r e 7 — S c a t t e r P l o t o f U n i c a s t T h r o u g h p u t . E a c h p o i n t r e p r e s e n t s t h e
t h r o u g h p u t o f a p a r t i c u l a r s o u r c e d e s t i n a t i o n p a i r . P o i n t s a b o v e t h e 4 5 - d e g r e e
l i n e i n d i c a t e i m p r o v e m e n t w i t h o p p o r t u n i s t i c r o u t i n g . T h e ﬁ g u r e s h o w s t h a t
o p p o r t u n i s t i c r o u t i n g i s p a r t i c u l a r l y b e n e ﬁ c i a l t o c h a l l e n g e d ﬂ o w s .
0
0 . 2
0 . 4
0 . 6
0 . 8
1
1 0 2 0 3 0 4 0 5 0 6 0 7 0
C u m u l a t i v e F r a c t i o n o f F l o w s
T h r o u g h p u t [ p k t / s ]
S r c r
E x O R
M O R E
F i g u r e 8 — S p a t i a l R e u s e . T h e ﬁ g u r e s h o w s C D F s o f u n i c a s t t h r o u g h p u t
a c h i e v e d b y M O R E , E x O R , a n d S r c r f o r ﬂ o w s t h a t t r a v e r s e 4 h o p s , w h e r e
t h e l a s t h o p c a n t r a n s m i t c o n c u r r e n t l y w i t h t h e ﬁ r s t h o p . M O R E ’ s m e d i a n
t h r o u g h p u t i s 4 5 % h i g h e r t h a n E x O R .
s p a t i a l r e u s e . T o e x a m i n e t h i s i s s u e c l o s e l y , w e f o c u s o n a f e w ﬂ o w s
t h a t w e k n o w c a n b e n e ﬁ t f r o m s p a t i a l r e u s e . E a c h ﬂ o w h a s a b e s t
p a t h o f 4 h o p s , w h e r e t h e l a s t h o p c a n s e n d c o n c u r r e n t l y w i t h t h e
ﬁ r s t h o p w i t h o u t c o l l i s i o n . F i g . 8 p l o t s t h e C D F o f t h r o u g h p u t o f t h e
t h r e e p r o t o c o l s f o r t h i s e n v i r o n m e n t . F o c u s i n g o n p a t h s w i t h s p a t i a l
r e u s e a m p l i ﬁ e s t h e g a i n M O R E h a s o v e r E x O R . T h e ﬁ g u r e s h o w s
t h a t f o r 4 - h o p ﬂ o w s w i t h s p a t i a l r e u s e , M O R E a c h i e v e s a 4 5 % h i g h e r
m e d i a n t h r o u g h p u t t h a n E x O R .
I t i s i m p o r t a n t t o n o t e t h a t s p a t i a l r e u s e m a y o c c u r e v e n f o r s h o r t e r
p a t h s . T h e c a p t u r e e f f e c t a l l o w s m u l t i p l e t r a n s m i s s i o n s t o b e c o r -
r e c t l y r e c e i v e d e v e n w h e n t h e n o d e s a r e w i t h i n t h e r a d i o r a n g e o f
b o t h s e n d e r s [ 3 2 ] . I n p a r t i c u l a r , l e s s t h a n 7 % o f t h e ﬂ o w s i n F i g . 6
h a v e a b e s t p a t h o f 4 h o p s o r l o n g e r . S t i l l M O R E d o e s b e t t e r t h a n
F i g u r e 9 — M u l t i c a s t T o p o l o g y . A s i m p l e t o p o l o g y u s e d i n t h e m u l t i c a s t
e x p e r i m e n t s i n F i g . 1 0 .
0
5 0
1 0 0
1 5 0
2 0 0
2 5 0
2 3 4
T h r o u g h p u t P e r D e s t i n a t i o n [ p k t / s ]
N u m b e r o f D e s t i n a t i o n s
S r c r
E x O R
M O R E
F i g u r e 1 0 — M u l t i c a s t T h r o u g h p u t a s a F u n c t i o n o f t h e N u m b e r o f D e s -
t i n a t i o n s f o r t h e T o p o l o g y i n F i g . 9 . T h e ﬁ g u r e s h o w s t h e p e r - d e s t i n a t i o n
m u l t i c a s t t h r o u g h p u t o f M O R E , E x O R , a n d S r c r . T h e t h i c k b a r s s h o w t h e
a v e r a g e p e r - d e s t i n a t i o n t h r o u g h p u t t a k e n o v e r 4 0 r u n s w i t h d i f f e r e n t n o d e s .
T h e l i n e s s h o w t h e s t a n d a r d d e v i a t i o n .
E x O R . T h i s i s m a i n l y b e c a u s e o f c a p t u r e . T h e c a p t u r e e f f e c t , h o w -
e v e r , i s h a r d t o q u a n t i f y o r m e a s u r e . T h u s , w e h a v e f o c u s e d o n l o n g e r
p a t h s t o s h o w t h e i m p a c t o f s p a t i a l r e u s e .
8 . 5 M u l t i c a s t
W e w a n t t o c o m p a r e t h e p e r f o r m a n c e o f m u l t i c a s t t r a f ﬁ c u n d e r
M O R E , E x O R , a n d S r c r . I n 7 , w e d e s c r i b e d h o w m u l t i c a s t w o r k s
u n d e r M O R E . I n c o n t r a s t , E x O R [ 7 ] a n d S r c r [ 6 ] d o n o t h a v e m u l -
t i c a s t e x t e n s i o n s . T h u s , w e n e e d t o d e ﬁ n e h o w t h e s e p r o t o c o l s d e a l
w i t h m u l t i c a s t . F o r S r c r w e a d o p t t h e s a m e a p p r o a c h a s w i r e d m u l -
t i c a s t . S p e c i ﬁ c a l l y , w e ﬁ n d t h e s h o r t e s t p a t h f r o m t h e s o u r c e t o e a c h
d e s t i n a t i o n , u s i n g E T X a s t h e m e t r i c . T h e s e p a t h s c r e a t e a t r e e r o o t e d
a t t h e s o u r c e . S r c r ’ s m u l t i c a s t t r a f ﬁ c i s s e n t a l o n g t h e b r a n c h e s o f t h i s
t r e e . I n c o n t r a s t , w i t h E x O R , w e w a n t m u l t i c a s t t r a f ﬁ c t o e x p l o i t o p -
p o r t u n i s t i c r e c e p t i o n s . W e ﬁ n d t h e E x O R f o r w a r d e r s f o r e a c h d e s -
t i n a t i o n . T h e p e r - d e s t i n a t i o n f o r w a r d e r s u s e t h e E x O R p r o t o c o l t o
a c c e s s t h e m e d i u m a n d c o o r d i n a t e t h e i r t r a n s m i s s i o n s . I n c o n t r a s t
t o u n i c a s t E x O R , i f t h e f o r w a r d e r s t o w a r d d e s t i n a t i o n X o p p o r t u n i s -
t i c a l l y h e a r a p a c k e t b y a f o r w a r d e r i n t h e f o r w a r d e r l i s t o f d e s t i -
n a t i o n Y , t h e y e x p l o i t t h a t o p p o r t u n i s t i c r e c e p t i o n . S a i d d i f f e r e n t l y ,
w e a l l o w o p p o r t u n i s t i c r e c e p t i o n s a c r o s s t h e f o r w a r d e r s o f v a r i o u s
d e s t i n a t i o n s .
O u r r e s u l t s s h o w t h a t M O R E ’ s m u l t i c a s t t h r o u g h p u t i s s i g n i ﬁ -
c a n t l y h i g h e r t h a n b o t h E x O R a n d S r c r . I n p a r t i c u l a r , w e e x p e r i m e n t
w i t h t h e s i m p l e t o p o l o g y i n F i g . 9 , w h e r e t h e s o u r c e m u l t i c a s t s a ﬁ l e
t o a v a r y i n g n u m b e r o f d e s t i n a t i o n s . F i g . 1 0 s h o w s t h e a v e r a g e m u l -
t i c a s t t h r o u g h p u t a s a f u n c t i o n o f t h e n u m b e r o f d e s t i n a t i o n s . T h e
a v e r a g e i s c o m p u t e d o v e r 4 0 d i f f e r e n t i n s t a n t i a t i o n s o f t h e t o p o l o g y
i n F i g 9 , u s i n g n o d e s i n o u r t e s t b e d . A s e x p e c t e d , t h e p e r - d e s t i n a t i o n
a v e r a g e t h r o u g h p u t d e c r e a s e s w i t h i n c r e a s e d n u m b e r o f d e s t i n a t i o n s .
I n t e r e s t i n g l y , h o w e v e r , t h e ﬁ g u r e s h o w s t h a t M O R E ’ s t h r o u g h p u t
g a i n i n c r e a s e s w i t h i n c r e a s e d n u m b e r o f d e s t i n a t i o n s . M O R E h a s
3 5 - 2 0 0 % t h r o u g h p u t g a i n o v e r E x O R a n d 1 0 0 - 3 0 0 % g a i n o v e r S r c r .
M O R E ’ s m u l t i c a s t t h r o u g h p u t g a i n i s h i g h e r t h a n i t s u n i c a s t g a i n .
T h i s i s b e c a u s e n e t w o r k c o d i n g ﬁ t s n a t u r a l l y w i t h m u l t i c a s t . R e c a l l
f r o m t h e e x a m p l e i n 2 t h a t w i t h o u t n e t w o r k c o d i n g , a t r a n s m i t t e r
Batch Size
0
0 . 2
0 . 4
0 . 6
0 . 8
1
0 5 0 1 0 0 1 5 0 2 0 0
C u m u l a t i v e F r a c t i o n o f F l o w s
T h r o u g h p u t [ p k t / s ]
M O R E , K = 8
M O R E , K = 1 6
M O R E , K = 3 2
M O R E , K = 6 4
M O R E , K = 1 2 8
( a ) M O R E
0
0 . 2
0 . 4
0 . 6
0 . 8
1
0 5 0 1 0 0 1 5 0 2 0 0
C u m u l a t i v e F r a c t i o n o f F l o w s
T h r o u g h p u t [ p k t / s ]
E x O R , K = 8
E x O R , K = 1 6
E x O R , K = 3 2
E x O R , K = 6 4
E x O R , K = 1 2 8
( b ) E x O R
F i g u r e 1 4 — I m p a c t o f B a t c h S i z e . T h e ﬁ g u r e s h o w s t h e C D F o f t h e
t h r o u g h p u t t a k e n o v e r 4 0 r a n d o m n o d e p a i r s . I t s h o w s t h a t M O R E i s l e s s
s e n s i t i v e t o t h e b a t c h s i z e t h a n E x O R .
c o n f u s i n g c o l l i s i o n d r o p s f r o m e r r o r d r o p s a n d u n n e c e s s a r i l y r e d u c -
i n g t h e b i t - r a t e .
A c l o s e e x a m i n a t i o n o f t h e t r a c e s i n d i c a t e s t h a t t h e a u t o - r a t e a l g o -
r i t h m o f t e n p i c k s t h e l o w e s t b i t - r a t e i n a n a t t e m p t t o r e d u c e p a c k e t
l o s s ; h o w e v e r , t h e i m p r o v e m e n t i n q u a l i t y o f t h e r e l a t i v e l y g o o d
l i n k s i s l i m i t e d , a n d a l a r g e f r a c t i o n o f t h e l o s s e s i s d u e t o i n t e r -
f e r e n c e t h u s c a n n o t b e a v o i d e d b y r e d u c i n g t h e b i t - r a t e . T h i s l i m -
i t e d b e n e ﬁ t i s g r e a t l y o u t w e i g h e d b y t h e s a c r i ﬁ c e i n b a n d w i d t h e f -
ﬁ c i e n c y . I n o u r e x p e r i m e n t s , t h e a v e r a g e s u c c e s s r a t e o f a l l t r a n s -
m i s s i o n s i m p r o v e s o n l y s l i g h t l y w i t h a u t o r a t e f r o m 6 6 % t o 6 8 % . A t
t h e s a m e t i m e , o n a v e r a g e 2 3 % o f a l l t r a n s m i s s i o n s u s i n g a u t o r a t e
a r e d o n e a t t h e l o w e s t b i t - r a t e , w h i c h t a k e s r o u g h l y 1 0 t i m e s l o n g e r
t h a n t h e h i g h e s t b i t - r a t e . T h e s e t r a n s m i s s i o n s f o r m a t h r o u g h p u t b o t -
t l e n e c k a n d c o n s u m e a l m o s t 7 0 % o f t h e s h a r e d m e d i u m t i m e . A s
s h o w n i n F i g . 1 3 , t h i s p r o b l e m a f f e c t s a b o u t 8 0 % o f a l l ﬂ o w s t e s t e d .
8 . 8 B a t c h S i z e
W e e x p l o r e t h e p e r f o r m a n c e o f M O R E a n d E x O R f o r v a r i o u s
b a t c h s i z e s . F i g . 1 4 p l o t s t h e t h r o u g h p u t f o r b a t c h s i z e s o f 8 , 1 6 , 3 2 ,
6 4 , a n d 1 2 8 . I t s h o w s t h a t E x O R ’ s p e r f o r m a n c e w i t h s m a l l b a t c h e s
o f 8 p a c k e t s i s s i g n i ﬁ c a n t l y w o r s e t h a n l a r g e b a t c h e s . I n c o n t r a s t ,
M O R E i s h i g h l y i n s e n s i t i v e t o d i f f e r e n t b a t c h s i z e s .
I n b o t h E x O R a n d M O R E , t h e o v e r h e a d i n c r e a s e s w i t h r e d u c e d
b a t c h s i z e . E x O R n o d e s e x c h a n g e c o n t r o l p a c k e t s w h e n e v e r t h e y
t r a n s m i t a b a t c h . I n c r e a s i n g t h e b a t c h s i z e a l l o w s E x O R t o a m o r t i z e
t h e c o n t r o l t r a f ﬁ c a n d r e d u c e s t h e c h a n c e o f s p u r i o u s t r a n s m i s s i o n s .
M O R E m a y m a k e a f e w s p u r i o u s t r a n s m i s s i o n s b e t w e e n t h e t i m e
t h e d e s t i n a t i o n d e c o d e s a b a t c h a n d w h e n t h e s o u r c e a n d f o r w a r d e r s
s t o p t r a n s m i t t i n g p a c k e t s f r o m t h a t b a t c h . A b i g g e r b a t c h s i z e a l l o w s
M O R E t o a m o r t i z e t h e c o s t o f t h e s e s p u r i o u s t r a n s m i s s i o n s o v e r a
l a r g e r n u m b e r o f p a c k e t s , i n c r e a s i n g t h e o v e r a l l t h r o u g h p u t .
I n s e n s i t i v i t y t o b a t c h s i z e s a l l o w s M O R E t o v a r y t h e b a t c h s i z e t o
a c c o m m o d a t e d i f f e r e n t t r a n s f e r s i z e s . W e e x p e c t t h a t f o r a n y t r a n s f e r
s i z e l a r g e r t h a n 7 - 1 0 p a c k e t s ( i . e . , a b a t c h l a r g e r t h a n 7 - 1 0 p a c k e t s ) ,
M O R E w i l l s h o w s i g n i ﬁ c a n t a d v a n t a g e s . S h o r t e r t r a n s f e r s c a n b e
O p e r a t i o n A v g . T i m e [ s ] S t d . D e v . [ s ]
I n d e p e n d e n c e c h e c k 1 0 5
C o d i n g a t t h e s o u r c e 2 7 0 1 5
D e c o d i n g 2 6 0 1 5 0
T a b l e 2 — A v e r a g e c o m p u t a t i o n a l c o s t o f p a c k e t o p e r a t i o n s i n M O R E .
T h e n u m b e r s f o r K 3 2 a n d 1 5 0 0 B p a c k e t s a r e m e a s u r e d o n a l o w - e n d
C e l e r o n m a c h i n e c l o c k e d a t 8 0 0 M H z w i t h 1 2 8 K i B c a c h e . N o t e t h a t t h e c o d -
i n g c o s t i s h i g h e s t a t t h e s o u r c e b e c a u s e i t h a s t o c o d e a l l K p a c k e t s t o g e t h e r .
T h e c o d i n g c o s t a t a f o r w a r d e r d e p e n d s o n t h e n u m b e r o f i n n o v a t i v e p a c k e t s
i t h a s r e c e i v e d , a n d i s a l w a y s b o u n d e d b y t h e c o d i n g c o s t a t t h e s o u r c e .
s e n t u s i n g t r a d i t i o n a l r o u t i n g . N o t e t h a t M O R E b e n i g n l y c o - e x i s t s
w i t h t r a d i t i o n a l r o u t i n g , w h i c h i t u s e s t o d e l i v e r i t s A C K s .
8 . 9 M O R E ’ s O v e r h e a d
F i n a l l y , w e w o u l d l i k e t o e s t i m a t e M O R E ’ s o v e r h e a d a n d i t s s u i t -
a b i l i t y f o r d e p l o y m e n t i n m e s h n e t w o r k s l i k e R o o f n e t [ 1 ] a n d c o m -
m u n i t y w i r e l e s s n e t w o r k s [ 3 4 , 3 ] .
( a ) C o d i n g O v e r h e a d : I n M O R E , t h e c o s t o f c o d i n g / d e c o d i n g p a c k -
e t s i s i n c u r r e d m a i n l y w h e n t h e p a c k e t h a s t o b e m u l t i p l i e d b y a r a n -
d o m n u m b e r ( i n a ﬁ n i t e ﬁ e l d o f s i z e 2
8
) . T o o p t i m i z e t h i s o p e r a t i o n ,
o u r i m p l e m e n t a t i o n r e d u c e s t h e c o s t b y u s i n g a 6 4 K i B l o o k u p - t a b l e
i n d e x e d b y p a i r s o f 8 b i t s . T h e l o o k u p t a b l e c a c h e s r e s u l t s o f a l l
p o s s i b l e m u l t i p l i c a t i o n s , s o m u l t i p l y i n g a n y b y t e o f a p a c k e t w i t h a
r a n d o m n u m b e r i s s i m p l y a f a s t l o o k u p .
T a b l e 2 p r o v i d e s m i c r o b e n c h m a r k s f o r c o d i n g a n d d e c o d i n g i n
M O R E . T h e m e a s u r e m e n t s a r e t a k e n o n a l o w - e n d C e l e r o n 8 0 0 M H z
m a c h i n e . T h e b e n c h m a r k s s h o w t h a t c o d i n g a n d d e c o d i n g h a v e
r o u g h l y e q u a l c o s t . T h e y r e q u i r e o n a v e r a g e K ﬁ n i t e - ﬁ e l d m u l t i p l i -
c a t i o n s p e r b y t e , w h e r e K i s t h e b a t c h s i z e . T h i s t i e s t h e c h o i c e o f
K w i t h t h e m a x i m u m a c h i e v a b l e t h r o u g h p u t . I n o u r s e t t i n g K 3 2
a n d c o d i n g t a k e s o n a v e r a g e 2 7 0 s p e r 1 5 0 0 B p a c k e t . T h i s l i m i t s t h e
e f f e c t i v e t h r o u g h p u t t o 4 4 M b / s , w h i c h i s h i g h e r t h a n t h e e f f e c t i v e
b i t r a t e o f c u r r e n t w i r e l e s s m e s h n e t w o r k s [ 2 0 ] .
( b ) M e m o r y O v e r h e a d : I n M O R E , l i k e i n E x O R , r o u t e r s d o n o t k e e p
a n o u t p u t q u e u e . I n s t e a d , t h e y s t o r e t h e c u r r e n t b a t c h f r o m e a c h ﬂ o w .
T h i s p e r - ﬂ o w s t a t e i s d o m i n a t e d b y t h e s t o r a g e r e q u i r e d t o b u f f e r
i n n o v a t i v e p a c k e t s f r o m t h e c u r r e n t b a t c h , w h i c h i s b o u n d e d b y
K 3 2 p a c k e t s . A d d i t i o n a l l y , a s s t a t e d a b o v e , M O R E n o d e s k e e p
a 6 4 K i B l o o k u p - t a b l e . G i v e n t h a t t h e n u m b e r o f c o n c u r r e n t ﬂ o w s
i n a m e s h n e t w o r k i s r e l a t i v e l y s m a l l , w e b e l i e v e M O R E ’ s m e m o r y
o v e r h e a d i s a c c e p t a b l e .
( c ) H e a d e r O v e r h e a d : M O R E ’ s h e a d e r i n o u r c u r r e n t i m p l e m e n t a -
t i o n i s b o u n d e d b y 7 0 b y t e s b e c a u s e w e b o u n d t h e n u m b e r o f f o r -
w a r d e r s t o 1 0 . C e r t a i n v a l u e s i n t h e h e a d e r a r e c o m p r e s s e d t o i n -
c r e a s e e f ﬁ c i e n c y . F o r e x a m p l e , s i n c e r o u t e r s o n l y k e e p t h e c u r r e n t
b a t c h , w e c a n r e p r e s e n t b a t c h I D s u s i n g a f e w b i t s . S i m i l a r l y , w e
c o m p r e s s t h e n o d e I D i n t h e f o r w a r d e r l i s t t o o n e b y t e , w h i c h i s a
h a s h o f i t s I P . T h i s w o r k s b e c a u s e o n l y n o d e s w h o s e E T X t o t h e
d e s t i n a t i o n i s s m a l l e r t h a n t h e s o u r c e a r e a l l o w e d t o p a r t i c i p a t e i n
f o r w a r d i n g . F o r 1 5 0 0 B p a c k e t s , t h e h e a d e r o v e r h e a d i s l e s s t h a n 5 % .
N o t e t h a t o u r t h r o u g h p u t n u m b e r s a r e c o m p u t e d o v e r t h e d e l i v e r e d
d a t a , a n d t h u s t h e y a l r e a d y a c c o u n t f o r h e a d e r o v e r h e a d .
N o t e t h a t t h e p r o b e p a c k e t s u s e d t o m e a s u r e l i n k l o s s p r o b a b i l i t i e s
d o n o t c o n s t i t u t e a M O R E - s p e c i ﬁ c o v e r h e a d . T h e s e p r o b a b i l i t i e s a r e
m e a s u r e d b y t h e a l l s t a t e - o f - a r t w i r e l e s s r o u t i n g p r o t o c o l s , i n c l u d i n g
E x O R [ 7 ] , a n d b e s t - p a t h [ 6 ] .
9 . C O N C L U S I O N
O p p o r t u n i s t i c r o u t i n g a n d n e t w o r k c o d i n g a r e t w o p o w e r f u l i d e a s
w h i c h m a y a t ﬁ r s t s i g h t a p p e a r u n r e l a t e d . O u r w o r k c o m b i n e s t h e s e
Throughput Dropoff
•Only every third node can transmit, or you get the
hidden terminal problem
•In TCP , data and ack packets cause the hidden
terminal problem
A B C D
A B C
data data
data ack

Bidirectional Network Coding (COPE, Katti
et al.) Coding
•Reed-Solomon codes for burst errors on small data
units
•LT codes for data delivery
•MORE for wireless communication
•General theme: being robust to individual losses
through mixing data and redundancy
•Layer 1 (Reed-Solomon), Layer 2.5 (MORE, COPE),
Layer 7 (LT)
