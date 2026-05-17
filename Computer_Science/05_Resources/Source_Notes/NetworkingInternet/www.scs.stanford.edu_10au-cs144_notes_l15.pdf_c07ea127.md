Title: l15.pdf
Mapped Topic: Network systems course notes
Source URL: https://www.scs.stanford.edu/10au-cs144/notes/l15.pdf
Source Type: university_course_notes
Trust Score: 95
Fetched At: 2026-04-17T06:57:53+00:00
Mapped From CSE.md Section: Part 1 / Part 2.B

# Content

Recall from last lecture
• To a ﬁrst approximation, attackers control network
• Next two lectures: How to defend against this
1. Communicate securely despite insecure networks – cryptography
2. Secure small parts of network despite wider Internet

Cryptography
• Crypto important tool for securing communication
- But often misused
- Have to understand what it guarantees and what it doesn’t

How Cryptography Helps
• Secrecy
- Encryption
• Integrity
- Cryptographic hashes
- Digital signatures
- Message authentication codes (MACs)
• Authentication
- Certiﬁcates, signatures, MACs
• Availability
- Can’t usually be guaranteed by cryptography alone

[Symmetric] Encryption
• Both parties share a secret key K
• Given a message M , and a key K :
- M is known as the plaintext
- E ( K, M ) → C ( C known as the ciphertext )
- D ( K, C ) → M
- Attacker cannot efﬁciently derive M from C without K
• Note E and D take same argument K
- Thus, also sometimes called symmetric encryption
- Raises issue of how to get K : more on that later
• Example algorithms: AES, Blowﬁsh, DES, RC4, . . .

One-time pad
• Share a completely random key K
• Encrypt M by XORing with K :
E ( K, M ) = M ⊕ K
• Decrypt by XORing again:
D ( K, C ) = C ⊕ K
• Advantage: Information-theoretically secure
- Given C but not K , any M of same length equally likely
- Also: fast!
• Disadvantage: K must be as long as M
- Makes distributing K for each message difﬁcult

Idea: Computational security
• Distribute small K securely (e.g., 128 bits)
• Use K to encrypt far larger M (e.g., 1 MByte ﬁle)
• Given C = E ( K, M ) , may be only one possible M
- If M has redundancy
• But believed computationally intractable to ﬁnd
- E.g., could try every possible K , but 2
128
keys a lot of work!

Types of encryption algorithms
• Stream ciphers – pseudo-random pad
- Generate pseudo-random stream of bits from short key
- Encrypt/decrypt by XORing with stream as if one-time pad
- But NOT one-time PAD! (People who claim so are frauds!)
- In practice, many stream ciphers uses have run into
problems
• More common algorithm type: Block cipher
- Operates on ﬁxed-size blocks (e.g., 64 or 128 bits)
- Maps plaintext blocks to same size ciphertext blocks
- Today should use AES; other algorithms: DES, Blowﬁsh, . . .

Example stream cipher (RC4)
• Initialization:
- S [0 . . . 255] ← permutation ⟨ 0 , . . . 255 ⟩ (based on key); i ← 0 ; j ← 0;
• Generating pseudo-random bytes:
i ← ( i + 1) mod 256;
j ← ( j + S [ i ]) mod 256;
swap S [ i ] ↔ S [ j ];
return S [( S [ i ] + S [ j ]) mod 256] ;

Example stream cipher (RC4)
• Initialization:
- S [0 . . . 255] ← permutation ⟨ 0 , . . . 255 ⟩ (based on key); i ← 0 ; j ← 0;
• Generating pseudo-random bytes:
i ← ( i + 1) mod 256;
j ← ( j + S [ i ]) mod 256;
swap S [ i ] ↔ S [ j ];
return S [( S [ i ] + S [ j ]) mod 256] ;

Example stream cipher (RC4)
• Initialization:
- S [0 . . . 255] ← permutation ⟨ 0 , . . . 255 ⟩ (based on key); i ← 0 ; j ← 0;
• Generating pseudo-random bytes:
i ← ( i + 1) mod 256;
j ← ( j + S [ i ]) mod 256;
swap S [ i ] ↔ S [ j ];
return S [( S [ i ] + S [ j ]) mod 256] ;

Example stream cipher (RC4)
• Initialization:
- S [0 . . . 255] ← permutation ⟨ 0 , . . . 255 ⟩ (based on key); i ← 0 ; j ← 0;
• Generating pseudo-random bytes:
i ← ( i + 1) mod 256;
j ← ( j + S [ i ]) mod 256;
swap S [ i ] ↔ S [ j ];
return S [( S [ i ] + S [ j ]) mod 256] ;

Example stream cipher (RC4)
• Initialization:
- S [0 . . . 255] ← permutation ⟨ 0 , . . . 255 ⟩ (based on key); i ← 0 ; j ← 0;
• Generating pseudo-random bytes:
i ← ( i + 1) mod 256;
j ← ( j + S [ i ]) mod 256;
swap S [ i ] ↔ S [ j ];
return S [( S [ i ] + S [ j ]) mod 256] ;

RC4 security
• Warning: Lecture goal just to give a feel
- May omit critical details necessary to use RC4 and other
algorithms securely
• RC4 Goal: Indistinguishable from random sequence
- Given part of the output stream, it should be intractable to
distinguish it from a truly random string
• Problems
- Second byte of RC4 is 0 with twice expected probability [MS01]
- Bad to use many related keys (see WEP 802.11b) [FMS01]
- Recommendation: Discard the ﬁrst 256 bytes of RC4 output
[RSA, MS]

Example use of stream cipher
• Pre-arrange to share secret s with web vendor
• Exchange payment information as follows
- Send: E ( s, “ Visa card #3273. . . ” )
- Receive: E ( s, “ Order conﬁrmed, have a nice day” )
• Now an eavesdropper can’t ﬁgure out your Visa #

Wrong!
• Let’s say an attacker has the following:
- c 1 = Encrypt( s, “ Visa card #3273. . . ” )
- c 2 = Encrypt( s, “ Order conﬁrmed, have a nice day” )
• Now compute:
- m ← c 1 ⊕ c 2 ⊕ “ Order conﬁrmed, have a nice day”
• Lesson: Never re-use keys with a stream cipher
- Similar lesson applies to one-time pads
(That’s why they’re called one-time pads.)

Wired Equivalent Privacy (WEP)
• Initial security standard for 802.11
- Serious weaknesses discovered: able to crack a connection in
minutes
- Replaced by WPA in 2003
• Stream cipher, basic mode uses 64-bit key: 40 bits are
ﬁxed and 24 bits are an initialization vector (IV),
speciﬁed in the packet
- One basic ﬂaw: if IV ever repeated (only 4 million packets),
then key is reused
- Many implementations would reset IV on reboot
• Other ﬂaws include IV collisions, altered packets, etc.

Example block cipher (blowﬁsh)
F
F
F
P1
P2
P16
P17P18
32 bit 32 bit
32 bit32 bit
32 bit
Plaintext
64 bit 32 bit32 bit
64 bit
Ciphertext
13 More Iterations
“Feistel network”
• Derive F and 18 subkeys
( P 1 . . . P 18 ) from key
• Divide plaintext block into
two halves, L 0 and R 0
• R i = L i − 1 ⊕ P i
L i = R i − 1 ⊕ F ( R i )
• R 17 = L 16 ⊕ P 17
L 17 = R 16 ⊕ P 18
• Output L 17 R 17 .
(Note: This is just to give an idea; it’s not a complete description)

Using a block cipher
• In practice, message may be more than one block
• Encrypt with ECB (electronic code book) mode:
- Split plaintext into blocks, and encrypt separately
Enc Enc Enc
c 1 c 2 c 3
m 1 m 2 m 3
- Attacker can’t decrypt any of the blocks; message secure
• Note: can re-use keys, unlike stream cipher
- Every block encrypted with cipher will be secure

Wrong!
• Attacker will learn of repeated plaintext blocks
- If transmitting sparse ﬁle, will know where non-zero
regions lie
• Example: Intercepting military instructions
- Most days, send encryption of “nothing to report.”
- On eve of battle, send “attack at dawn.”
- Attacker will know when battle plans are being made

Another example [Preneel]

Cipher-block chaining (CBC)
IV
Enc Enc Enc
m 1 m 2 m 3
c 1 c 2 c 3
• Choose initialization vector (IV) for each message
- Can be 0 if key only ever used to encrypt one message
- Choose randomly for each message if key re-used
- Can be publicly known (e.g., transmit openly with ciphertext)
• c 1 = E ( K, m i ⊕ IV ) , c i = E ( K, m i ⊕ c i − 1 )
- Ensures repeated blocks are not encrypted the same

Encryption modes
• CBC, ECB are encryption modes, but there are others
• Cipher Feedback (CFB) mode: c i = m i ⊕ E ( K, c i − 1 )
- Useful for messages that are not multiple of block size
• Output Feedback (OFB) mode:
- Repeatedly encrypt IV & use result like stream cipher
• Counter (CTR) mode: c i = m i ⊕ E ( K, i )
- Useful if you want to encrypt in parallel
• Q: Given a shared key, can you transmit ﬁles securely
over net by just encrypting them in CBC mode?

2-minute break

Problem: Integrity
• Attacker can tamper with messages
- E.g., corrupt a block to ﬂip a bit in next
• What if you delete original ﬁle after transfer?
- Might have nothing but garbage at recipient
• Encryption does not guarantee integrity
- A system that uses encryption alone (no integrity check) is
often incorrectly designed.
- Exception: Cryptographic storage (to protect disk if stolen)

Message authentication codes
• Message authentication codes (MACs)
- Sender & receiver share secret key K
- For message m , compute v ← MAC ( K, m )
- Recipient runs CHECK ( K, v, m ) → { yes , no }
- Intractable to produce valid ⟨ m, v ⟩ without K
• To send message securely, append MAC
- Send { m, MAC ( K, m ) } ( m could be ciphertext, E ( K
′
, M ) )
- Receiver of { m, v } discards unless CHECK ( K, v, m ) = yes
• Careful of Replay – don’t believe previous { m, v }

Cryptographic hashes
• Hash arbitrary-length input to ﬁxed-size output
- Typical output size 160–512 bits
- Cheap to compute on large input (faster than network)
• Collision-resistant: Intractable to ﬁnd
x ̸= y such that H ( x ) = H ( y )
- Of course, many such collisions exist
- But no one has been able to ﬁnd one, even after analyzing
the algorithm
• Historically most popular hash SHA-1
- [Nearly] broken
- Today should use SHA-256 or SHA-512
- Competition underway for new hash standard

Applications of cryptographic hashes
• Small hash uniquely speciﬁes large data
- Hash a ﬁle, remember the hash value
- Recompute hash later, if same value no tampering
- Hashes often published for software distribution
• Hash tree [Merkle] lets you check small piece of large
ﬁle or database with log number of nodes
H
m 0 m 1 m 2 m 3 m 4 m 5 m 6 m 7

HMAC
• Use cryptographic hash to produce MAC
• HMAC ( K, m ) = H ( K ⊕ opad , H ( K ⊕ ipad , m ))
- H is a cryptographic hash such as SHA-1
- ipad is 0x36 repeated 64 times, opad 0x5c repeated 64 times
• To verify, just recompute HMAC
- CHECK ( K, v, m ) =
(
v
?
= HMAC ( K, m )
)
- Many MACs are deterministic and work like this (“PRFs”),
but fastest MACs randomized so CHECK can’t just recompute
• Note: Don’t just use H(K,M) as a MAC
- Say you have { M, SHA-1( K, M ) } , but not K
- Can produce { M
′
, SHA-1( K, M
′
) } where M
′
̸= M
- Hashes provide collision resistance, but do not prevent
spooﬁng new messages

Order of Encryption and MACs
• Should you Encrypt then MAC, or vice versa?
• MACing encrypted data is always secure
• Encrypting { Data+MAC } may not be secure!
- Consider the following secure, but stupid encryption alg
- Transform m → m
′
by mapping each bit to two bits:
Map 0 → 00 (always), 1 → { 10 , 01 } (randomly pick one)
- Now encrypt m
′
with a stream cipher to produce c
- Attacker ﬂips two bits of c —if msg rejected, was 0 bit in m

Public key encryption
• Three randomized algorithms:
- Generate – G (1
k
) → K, K
− 1
(randomized)
- Encrypt – E ( K, m ) → { m } K (randomized)
- Decrypt – D ( K
− 1
, { m } K ) → m
• Provides secrecy, like conventional encryption
- Can’t derive m from { m } K without knowing K
− 1
• Encryption key K can be made public
- Can’t derive K
− 1
from K
- Everyone can use same pub. key to encrypt for one recipient
• Note: Encrypt must be randomized
- Same message must encrypt to different ciphertext each time
- Otherwise, can easily guess plaintext from small message space
(E.g., encrypt “yes”, encrypt “no”, see which matches message)

Digital signatures
• Three (randomized) algorithms:
- Generate – G (1
k
) → K, K
− 1
(randomized)
- Sign – S
(
K
− 1
, m
)
→ { m } K
− 1 (can be randomized)
- Verify – V ( K, { m } K
− 1 , m ) → { yes , no }
• Provides integrity, like a MAC
- Cannot produce valid ⟨ m, { m } K
− 1 ⟩ pair without K
− 1
- But only need K to verify; cannot derive K
− 1
from K
- So K can be publicly known

Popular public key algorithms
• Encryption: RSA, Rabin, ElGamal
• Signature: RSA, Rabin, ElGamal, Schnorr, DSA, . . .
• Warning: Message padding critically important
- E.g., basic idea behind RSA encryption simple
- Just modular exponentiation of large integers
- But simple transformations of messages to numbers not secure
• Many keys support both signing & encryption
- But Encrypt/Decrypt and Sign/Verify different algorithms!
- Common error: Sign by “encrypting” with private key

Cost of cryptographic operations
• Cost of public key algorithms signiﬁcant
- E.g., encrypt or sign only ∼ 100 msgs/sec
- Can only encrypt small messages ( < size of key)
- Signature cost relatively insensitive to message size
- Some algorithm variants provide faster encrypt/verify
(e.g., Rabin, RSA-3 can encrypt ∼ 10 , 000 msgs/sec)
• In contrast, symmetric algorithms much cheaper
- Symmetric can encrypt+MAC faster than 1Gbps/sec LAN

Hybrid schemes
• Use public key to encrypt symmetric key
- Send message symmetrically encrypted: { msg } K S
, { K S } K P
• Use PK to negotiate secret session key
- Use Public Key crypto to establish 4 keys symmetric keys
- Client sends server: {{ m 1 } K 1
, MAC( K 2 , { m 1 } K 1
) }
- Server sends client: {{ m 2 } K 3
, MAC( K 4 , { m 2 } K 3
) }
• Often want mutual authentication (client & server)
- Or more complex, user(s), client, & server
• Common pitfall: signing underspeciﬁed messages
- E.g., Always specify intended recipient in signed messages
- Should also specify expiration, or better yet fresh data
- Otherwise like signing a blank check. . .

Server authentication
• Often want to communicate securely with a server
• Easy once you have server’s public key
- Use public key to bootstrap symmetric keys
• Problem: Key management
- How to get server’s public key?
- How to know the key is really server’s?

Danger: impersonating servers
Attacker
Client Server
• Attacker pretends to be server, gives its own pub key
• Attacker mounts man-in-the-middle attack
- Looks just like server to client (except for different public key)
- Attacker sees, then re-encrypts sensitive communications
- Attacker can also send bad data back to client

One solution: Certiﬁcate authorities (CAs)
1. PubKey, $$$
2. Certificate
3. Connection request
4. PubKey, Certificate
Client
Authority
Certification
Server
• Everybody trusts some certiﬁcate authority
• Everybody knows CA’s public key
- E.g., built into web browser
• This is how HTTPS (over SSL/TLS) works
- Active when you see padlock in your web browser

Digital certiﬁcates
• A digital certiﬁcate binds a public key to name
- E.g., “ www.ebay.com ’s public key is 0x39f32641. . . ”
- Digitally signed with a CA’s private key
• Certiﬁcates can be chained
- E.g., start with root CAs like Verisign
- Verisign can sign Stanford’s public key
- Stanford can sign keys for cs.stanford.edu , etc.
- Not as widely supported as it should be
(Maybe because CAs want $300 for every Stanford server)
• Assuming you trust the CA, solves the key
management problem

Another solution: Use passwords
• User remembers a password to authenticate himself
- Server stores password or secret derived from password
- Can then use password to authenticate server to client, as well
• Simplest example:
Client Server
MAC (password , pubkey)
• Big limitations of above (simple) protocol:
- Users choose weak passwords
- Since pubkey known, attacker gets one message from server,
then guess all common passwords ofﬂine
- Also, users employ same passwords at multiple sites
• Limitations addressed by fancier crypto protocols
- E.g., SRP , PAKE
+
2 protocols developed here at Stanford
