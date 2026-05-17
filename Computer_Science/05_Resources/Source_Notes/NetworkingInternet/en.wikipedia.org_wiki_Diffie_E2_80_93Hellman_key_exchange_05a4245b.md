Title: Diffie–Hellman key exchange - Wikipedia
Mapped Topic: Internet performance context
Source URL: https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange
Source Type: open_book
Trust Score: 93
Fetched At: 2026-04-17T07:00:31+00:00
Mapped From CSE.md Section: Part 1 / Part 2.B

# Content

# Diffie–Hellman key exchange

**Diffie–Hellman** (**DH**) **key exchange** [nb 1] is a mathematical method of securely generating a symmetric

[cryptographic key](https://en.wikipedia.org/wiki/Cryptographic_key)over a public channel and was one of the first

[protocols](https://en.wikipedia.org/wiki/Public-key_cryptography)as conceived by

[Ralph Merkle](https://en.wikipedia.org/wiki/Ralph_Merkle)and named after

[Whitfield Diffie](https://en.wikipedia.org/wiki/Whitfield_Diffie)and

[Martin Hellman](https://en.wikipedia.org/wiki/Martin_Hellman).

DH is one of the earliest practical examples of public key exchange implemented within the field of cryptography. Published in 1976 by Diffie and Hellman, this is the earliest publicly known work that proposed the idea of a private key and a corresponding public key.

[[1]](https://en.wikipedia.org#cite_note-Merkle_1978-2)Traditionally, secure encrypted communication between two parties required that they first exchange keys by some secure physical means, such as paper key lists transported by a trusted [courier](https://en.wikipedia.org/wiki/Courier). The Diffie–Hellman key exchange method allows two parties that have no prior knowledge of each other to jointly establish a [shared secret](https://en.wikipedia.org/wiki/Shared_secret) key over an [insecure channel](https://en.wikipedia.org/wiki/Insecure_channel). This key can then be used to encrypt subsequent communications using a [symmetric-key](https://en.wikipedia.org/wiki/Symmetric-key_algorithm) [cipher](https://en.wikipedia.org/wiki/Cipher).

Diffie–Hellman is used to secure a variety of [Internet](https://en.wikipedia.org/wiki/Internet) services. However, research published in October 2015 suggests that the parameters in use for many DH Internet applications at that time are not strong enough to prevent compromise by very well-funded attackers, such as the security services of some countries.[[2]](https://en.wikipedia.org#cite_note-imperfectfs-3)

The scheme was published by Whitfield Diffie and Martin Hellman in 1976, [3] but in 1997 it was revealed that

[James H. Ellis](https://en.wikipedia.org/wiki/James_H._Ellis),

[[4]](https://en.wikipedia.org#cite_note-5)[Clifford Cocks](https://en.wikipedia.org/wiki/Clifford_Cocks), and

[Malcolm J. Williamson](https://en.wikipedia.org/wiki/Malcolm_J._Williamson)of

[GCHQ](https://en.wikipedia.org/wiki/Government_Communications_Headquarters), the British signals intelligence agency, had previously shown in 1969

how public-key cryptography could be achieved.

[[5]](https://en.wikipedia.org#cite_note-6)

[[6]](https://en.wikipedia.org#cite_note-7)Although Diffie–Hellman key exchange itself is a non-authenticated [key-agreement protocol](https://en.wikipedia.org/wiki/Key-agreement_protocol), it provides the basis for a variety of authenticated protocols, and is used to provide [forward secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) in [Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security)'s [ephemeral](https://en.wikipedia.org/wiki/Ephemeral_key) modes (referred to as EDH or DHE depending on the cipher suite). Forward secrecy results from the use of ephemeral keys: the private keys are discarded once key agreement is complete, making them safe from later compromise. Ephemeral keys are practical because it is computationally cheap to create public-private key pairs suitable for use with Diffie-Hellman exchange.

The method was followed shortly after by the [RSA cryptosystem](https://en.wikipedia.org/wiki/RSA_cryptosystem), an implementation of public-key cryptography using asymmetric algorithms.

Expired US patent 4200770 [7] from 1977 describes the now public-domain algorithm. It credits Hellman, Diffie, and Merkle as inventors.

## Name

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=1)]

In 2006, Hellman suggested the algorithm be called **Diffie–Hellman–Merkle key exchange** in recognition of [Ralph Merkle](https://en.wikipedia.org/wiki/Ralph_Merkle)'s contribution to the invention of [public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) (Hellman, 2006), writing:

The system ... has since become known as Diffie–Hellman key exchange. While that system was first described in a paper by Diffie and me, it is a public key distribution system, a concept developed by Merkle, and hence should be called 'Diffie–Hellman–Merkle key exchange' if names are to be associated with it. I hope this small pulpit might help in that endeavor to recognize Merkle's equal contribution to the invention of public key cryptography.

[[8]]

## Description

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=2)]

### General overview

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=3)]

Diffie–Hellman key exchange establishes a shared secret between two parties that can be used for secret communication for exchanging data over a public network. An analogy illustrates the concept of public key exchange by using colors instead of very large numbers:

The process begins by having the two parties, [Alice and Bob](https://en.wikipedia.org/wiki/Alice_and_Bob), publicly agree on an arbitrary starting color that does not need to be kept secret. In this example, the color is yellow. Each person also selects a secret color that they keep to themselves – in this case, red and cyan. The crucial part of the process is that Alice and Bob each mix their own secret color together with their mutually shared color, resulting in orange-tan and light-blue mixtures respectively, and then publicly exchange the two mixed colors. Finally, each of them mixes the color they received from the partner with their own private color. The result is a final color mixture (yellow-brown in this case) that is identical to their partner's final color mixture.

If a third party listened to the exchange, they would only know the common color (yellow) and the first mixed colors (orange-tan and light-blue), but it would be very hard for them to find out the final secret color (yellow-brown). Bringing the analogy back to a [real-life](https://en.wikipedia.org/wiki/Real-life) exchange using large numbers rather than colors, this determination is computationally expensive; it is impossible to compute in a practical amount of time even for modern [supercomputers](https://en.wikipedia.org/wiki/Supercomputer).

### Cryptographic explanation

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=4)]

The simplest and the original implementation, [3] later formalized as

**Finite Field Diffie–Hellman**in RFC 7919,

of the protocol uses the

[[9]](https://en.wikipedia.org#cite_note-10)[multiplicative group of integers modulo](https://en.wikipedia.org/wiki/Multiplicative_group_of_integers_modulo_n)

*p*, where

*p*is

[prime](https://en.wikipedia.org/wiki/Prime_number), and

*g*is a

[primitive root modulo](https://en.wikipedia.org/wiki/Primitive_root_modulo_n)

*p*. To guard against potential vulnerabilities, it is recommended to use prime numbers of at least 2048 bits in length. This increases the difficulty for an adversary attempting to compute the discrete logarithm and compromise the shared secret. These two values are chosen in this way to ensure that the resulting shared secret can take on any value from 1 to

*p*− 1. Here is an example of the protocol, with non-secret values in blue, and secret values in

**red**.

[Alice and Bob](https://en.wikipedia.org/wiki/Alice_and_Bob)publicly agree to use a modulus*p*= 23 and base*g*= 5 (which is a primitive root modulo 23).- Alice chooses a secret integer
= 4, then sends Bob**a***A*=*g*mod**a***p**A*= 5mod 23 = 4 (in this example both**4***A*andhave the same value 4, but this is usually not the case)**a**

- Bob chooses a secret integer
= 3, then sends Alice**b***B*=*g*mod**b***p**B*= 5mod 23 = 10**3**

- Alice computes
=**s***B*mod**a***p*= 10**s**mod 23 =**4****18**

- Bob computes
=**s***A*mod**b***p*= 4**s**mod 23 =**3****18**

- Alice and Bob now share a secret (the number 18).

Both Alice and Bob have arrived at the same values because under mod *p*,

More specifically,

Only *a* and *b* are kept secret. All the other values – *p*, *g*, *g a* mod

*p*, and

*g*mod

b*p*– are sent in the clear. The strength of the scheme comes from the fact that

*g*mod

ab*p*=

*g*mod

ba*p*take extremely long times to compute by any known classical algorithm just from the knowledge of

*p*,

*g*,

*g*mod

a*p*, and

*g*mod

b*p*. Such a function that is easy to compute but hard to invert is called a

[one-way function](https://en.wikipedia.org/wiki/One-way_function). Once Alice and Bob compute the shared secret they can use it as an encryption key, known only to them, for sending messages across the same open communications channel.

Of course, much larger values of *a*, *b*, and *p* would be needed to make this example secure, since there are only 23 possible results of *n* mod 23. However, if *p* is a prime of at least 600 digits, then even the fastest modern computers using the fastest known algorithm cannot find *a* given only *g*, *p* and *g a* mod

*p*. Such a problem is called the

[discrete logarithm problem](https://en.wikipedia.org/wiki/Discrete_logarithm_problem).

The computation of

[[2]](https://en.wikipedia.org#cite_note-imperfectfs-3)*g*mod

a*p*is known as

[modular exponentiation](https://en.wikipedia.org/wiki/Modular_exponentiation)and can be done efficiently even for large numbers. Note that

*g*need not be large at all, and in practice is usually a small integer (like 2, 3, ...).

### Secrecy chart

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=5)]

The chart below depicts who knows what, again with non-secret values in blue, and secret values in **red**. Here [Eve](https://en.wikipedia.org/wiki/Alice_and_Bob#Cast_of_characters) is an [eavesdropper](https://en.wikipedia.org/wiki/Eavesdropping#Network_attacks) – she watches what is sent between Alice and Bob, but she does not alter the contents of their communications.

*g*, public (primitive root) base, known to Alice, Bob, and Eve.*g*= 5*p*, public (prime) modulus, known to Alice, Bob, and Eve.*p*= 23, Alice's private key, known only to Alice.**a**=**a****6**, Bob's private key known only to Bob.**b**=**b****15***A*, Alice's public key, known to Alice, Bob, and Eve.*A*=*g*mod**a***p*= 8*B*, Bob's public key, known to Alice, Bob, and Eve.*B*=*g*mod**b***p*= 19

|
|
|

Now * s* is the shared secret key and it is known to both Alice and Bob, but

*not*to Eve. Note that it is not helpful for Eve to compute

*AB*, which equals

*g*

mod p.

*+***a****b**Note: It should be difficult for Alice to solve for Bob's private key or for Bob to solve for Alice's private key. If it is not difficult for Alice to solve for Bob's private key (or vice versa), then an eavesdropper, [Eve](https://en.wikipedia.org/wiki/Alice_and_Bob#Cast_of_characters), may simply substitute her own private / public key pair, plug Bob's public key into her private key, produce a fake shared secret key, and solve for Bob's private key (and use that to solve for the shared secret key). [Eve](https://en.wikipedia.org/wiki/Alice_and_Bob#Cast_of_characters) may attempt to choose a public / private key pair that will make it easy for her to solve for Bob's private key.

### Generalization to finite cyclic groups

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=6)]

Here is a more general description of the protocol:[[10]](https://en.wikipedia.org#cite_note-11)

- Alice and Bob agree on a natural number
*n*and a[generating](https://en.wikipedia.org/wiki/Generating_set_of_a_group)element*g*in the finite[cyclic group](https://en.wikipedia.org/wiki/Cyclic_group)*G*of order*n*. (This is usually done long before the rest of the protocol;*g*and*n*are assumed to be known by all attackers.) The group*G*is written multiplicatively. - Alice picks a random
[natural number](https://en.wikipedia.org/wiki/Natural_number)*a*with 1 <*a*<*n*, and sends the element*g*ofa*G*to Bob. - Bob picks a random natural number
*b*with 1 <*b*<*n*, and sends the element*g*ofb*G*to Alice. - Alice computes the element (
*g*)b=*a**g*of G.ba - Bob computes the element (
*g*)a=*b**g*of G.ab

Both Alice and Bob are now in possession of the group element *g ab* =

*g*, which can serve as the shared secret key. The group

ba*G*satisfies the requisite condition for

[secure communication](https://en.wikipedia.org/wiki/Secure_communication)as long as there is no efficient algorithm for determining

*g*given

ab*g*,

*g*, and

a*g*.

bFor example, the [elliptic curve Diffie–Hellman](https://en.wikipedia.org/wiki/Elliptic-curve_Diffie%E2%80%93Hellman) protocol is a variant that represents an element of G as a point on an elliptic curve instead of as an integer modulo n. Variants using [hyperelliptic curves](https://en.wikipedia.org/wiki/Hyperelliptic_curve_cryptography) have also been proposed. The [supersingular isogeny key exchange](https://en.wikipedia.org/wiki/Supersingular_isogeny_key_exchange) is a Diffie–Hellman variant that was designed to be secure against [quantum computers](https://en.wikipedia.org/wiki/Quantum_computers), but it was broken in July 2022.[[11]](https://en.wikipedia.org#cite_note-castryckdecru2023-12)

## Ephemeral and/or static keys

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=7)]

The used keys can either be ephemeral or static (long term) key, but could even be mixed, so called semi-static DH. These variants have different properties and hence different use cases. An overview over many variants and some also discussions can for example be found in NIST SP 800-56A. [12] A basic list:

- ephemeral, ephemeral: Usually used for key agreement. Provides
[forward secrecy](https://en.wikipedia.org/wiki/Forward_secrecy), but no[authenticity](https://en.wikipedia.org/wiki/Authentication). - static, static: Would generate a long term shared secret. Does not provide forward secrecy, but implicit authenticity. Since the keys are static it would for example not protect against
[replay-attacks](https://en.wikipedia.org/wiki/Replay_attack). - ephemeral, static: For example, used in
[ElGamal encryption](https://en.wikipedia.org/wiki/ElGamal_encryption)or[Integrated Encryption Scheme (IES)](https://en.wikipedia.org/wiki/Integrated_Encryption_Scheme). If used in key agreement it could provide implicit one-sided authenticity (the ephemeral side could verify the authenticity of the static side). No forward secrecy is provided.

It is possible to use ephemeral and static keys in one key agreement to provide more security as for example shown in NIST SP 800-56A, but it is also possible to combine those in a single DH key exchange, which is then called triple DH (3-DH).

### Triple Diffie–Hellman (3-DH)

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=8)]

In 1997 a kind of triple DH was proposed by Simon Blake-Wilson, Don Johnson and Alfred Menezes, [13] which was improved by C. Kudla and K. G. Paterson in 2005

and shown to be secure.

[[14]](https://en.wikipedia.org#cite_note-15)The long term secret keys of Alice and Bob are denoted by *a* and *b* respectively, with public keys *A* and *B*, as well as the ephemeral key pairs (*x*, *X*) and (*y*, *Y*). Then protocol is:

| Alice () | Bob () | |
|---|---|---|

The long term public keys need to be transferred somehow. That can be done beforehand in a separate, trusted channel, or the public keys can be encrypted using some partial key agreement to preserve anonymity. For more of such details as well as other improvements like [side channel protection](https://en.wikipedia.org/wiki/Side-channel_attack) or explicit [key confirmation](https://en.wikipedia.org/wiki/Key_(cryptography)), as well as early messages and additional password authentication, see e.g. US patent "Advanced modular handshake for key agreement and optional authentication".[[15]](https://en.wikipedia.org#cite_note-16)

### Extended Triple Diffie–Hellman (X3DH)

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=9)]

X3DH was initially proposed as part of the [Double Ratchet Algorithm](https://en.wikipedia.org/wiki/Double_Ratchet_Algorithm) used in the [Signal Protocol](https://en.wikipedia.org/wiki/Signal_Protocol). The protocol offers forward secrecy and cryptographic deniability. It operates on an elliptic curve.[[16]](https://en.wikipedia.org#cite_note-x3dh-17)

The protocol uses five public keys. Alice has an identity key IKA and an ephemeral key EKA. Bob has an identity key IKB, a signed prekey SPKB, and a one-time prekey OPKB. [16] Bob first publishes his three keys to a server, which Alice downloads and verifies the signature on. Alice then initiates the exchange to Bob.

The OPK is optional.

[[16]](https://en.wikipedia.org#cite_note-x3dh-17)

[[16]](https://en.wikipedia.org#cite_note-x3dh-17)## Operation with more than two parties

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=10)]

Diffie–Hellman key agreement is not limited to negotiating a key shared by only two participants. Any number of users can take part in an agreement by performing iterations of the agreement protocol and exchanging intermediate data (which does not itself need to be kept secret). For example, Alice, Bob, and Carol could participate in a Diffie–Hellman agreement as follows, with all operations taken to be modulo *p*:

- The parties agree on the algorithm parameters
*p*and*g*. - The parties generate their private keys, named
*a*,*b*, and*c*. - Alice computes
`g`moda`p`and sends it to Bob. - Bob computes (
`g`)amod`b``p`=`g`modab`p`and sends it to Carol. - Carol computes (
`g`)abmod`c``p`=`g`modabc`p`and uses it as her secret. - Bob computes g
bmod`p`and sends it to Carol. - Carol computes (
`g`)bmod`c``p`=`g`modbc`p`and sends it to Alice. - Alice computes (
`g`)bcmod`a``p`=`g`modbca`p`=`g`modabc`p`and uses it as her secret. - Carol computes
`g`modc`p`and sends it to Alice. - Alice computes (
`g`)cmod`a``p`=`g`modca`p`and sends it to Bob. - Bob computes (
`g`)camod`b``p`=`g`modcab`p`=`g`modabc`p`and uses it as his secret.

An eavesdropper has been able to see `g a` mod

`p`,

`g`mod

b`p`,

`g`mod

c`p`,

`g`mod

ab`p`,

`g`mod

ac`p`, and

`g`mod

bc`p`, but cannot use any combination of these to efficiently reproduce

`g`mod

abc`p`.

To extend this mechanism to larger groups, two basic principles must be followed:

- Starting with an "empty" key consisting only of
*g*, the secret is made by raising the current value to every participant's private exponent once, in any order (the first such exponentiation yields the participant's own public key). - Any intermediate value (having up to
*N*−1 exponents applied, where*N*is the number of participants in the group) may be revealed publicly, but the final value (having had all*N*exponents applied) constitutes the shared secret and hence must never be revealed publicly. Thus, each user must obtain their copy of the secret by applying their own private key last (otherwise there would be no way for the last contributor to communicate the final key to its recipient, as that last contributor would have turned the key into the very secret the group wished to protect).

These principles leave open various options for choosing in which order participants contribute to keys. The simplest and most obvious solution is to arrange the *N* participants in a circle and have *N* keys rotate around the circle, until eventually every key has been contributed to by all *N* participants (ending with its owner) and each participant has contributed to *N* keys (ending with their own). However, this requires that every participant perform *N* modular exponentiations.

By choosing a more desirable order, and relying on the fact that keys can be duplicated, it is possible to reduce the number of modular exponentiations performed by each participant to log2(*N*) + 1 using a [divide-and-conquer-style](https://en.wikipedia.org/wiki/Divide_and_conquer_algorithms) approach, given here for eight participants:

- Participants A, B, C, and D each perform one exponentiation, yielding
`g`; this value is sent to E, F, G, and H. In return, participants A, B, C, and D receiveabcd`g`.efgh - Participants A and B each perform one exponentiation, yielding
`g`, which they send to C and D, while C and D do the same, yieldingefghab`g`, which they send to A and B.efghcd - Participant A performs an exponentiation, yielding
`g`, which it sends to B; similarly, B sendsefghcda`g`to A. C and D do similarly.efghcdb - Participant A performs one final exponentiation, yielding the secret
`g`=efghcdba`g`, while B does the same to getabcdefgh`g`=efghcdab`g`; again, C and D do similarly.abcdefgh - Participants E through H simultaneously perform the same operations using
`g`as their starting point.abcd

Once this operation has been completed all participants will possess the secret `g abcdefgh`, but each participant will have performed only four modular exponentiations, rather than the eight implied by a simple circular arrangement.

## Security and practical considerations

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=11)]

The protocol is considered secure against eavesdroppers if *G* and *g* are chosen properly. In particular, the order of the group G must be large, particularly if the same group is used for large amounts of traffic. The eavesdropper has to solve the [Diffie–Hellman problem](https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_problem) to obtain *g* ab. This is currently considered difficult for groups whose order is large enough. An efficient algorithm to solve the

[discrete logarithm problem](https://en.wikipedia.org/wiki/Discrete_logarithm_problem)would make it easy to compute

*a*or

*b*and solve the Diffie–Hellman problem, making this and many other public key cryptosystems insecure. Fields of small characteristic may be less secure.

[[17]](https://en.wikipedia.org#cite_note-18)The [order](https://en.wikipedia.org/wiki/Order_(group_theory)) of *G* should have a large prime factor to prevent use of the [Pohlig–Hellman algorithm](https://en.wikipedia.org/wiki/Pohlig%E2%80%93Hellman_algorithm) to obtain *a* or *b*. For this reason, a [Sophie Germain prime](https://en.wikipedia.org/wiki/Sophie_Germain_prime) *q* is sometimes used to calculate *p* = 2*q* + 1, called a [safe prime](https://en.wikipedia.org/wiki/Safe_prime), since the order of *G* is then only divisible by 2 and *q*. Sometimes *g* is chosen to generate the order *q* subgroup of *G*, rather than *G*, so that the [Legendre symbol](https://en.wikipedia.org/wiki/Legendre_symbol) of *g a* never reveals the low order bit of

*a*. A protocol using such a choice is for example

[IKEv2](https://en.wikipedia.org/wiki/Internet_Key_Exchange).

[[18]](https://en.wikipedia.org#cite_note-19)The generator *g* is often a small integer such as 2. Because of the [random self-reducibility](https://en.wikipedia.org/wiki/Random_self-reducibility) of the discrete logarithm problem a small *g* is equally secure as any other generator of the same group.

If Alice and Bob use [random number generators](https://en.wikipedia.org/wiki/Random_number_generator) whose outputs are not completely random and can be predicted to some extent, then it is much easier to eavesdrop.

In the original description, the Diffie–Hellman exchange by itself does not provide [authentication](https://en.wikipedia.org/wiki/Authentication) of the communicating parties and can be vulnerable to a [man-in-the-middle attack](https://en.wikipedia.org/wiki/Man-in-the-middle_attack).
Mallory (an active attacker executing the man-in-the-middle attack) may establish two distinct key exchanges, one with Alice and the other with Bob, effectively masquerading as Alice to Bob, and vice versa, allowing her to decrypt, then re-encrypt, the messages passed between them. Note that Mallory must be in the middle from the beginning and continuing to be so, actively decrypting and re-encrypting messages every time Alice and Bob communicate. If she arrives after the keys have been generated and the encrypted conversation between Alice and Bob has already begun, the attack cannot succeed. If she is ever absent, her previous presence is then revealed to Alice and Bob. They will know that all of their private conversations had been intercepted and decoded by someone in the channel. In most cases it will not help them get Mallory's private key, even if she used the same key for both exchanges.

A method to authenticate the communicating parties to each other is generally needed to prevent this type of attack. Variants of Diffie–Hellman, such as [STS protocol](https://en.wikipedia.org/wiki/Station-to-Station_protocol), may be used instead to avoid these types of attacks.

### Denial-of-service attack

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=12)]

A [CVE](https://en.wikipedia.org/wiki/Common_Vulnerabilities_and_Exposures) released in 2021 (* CVE-2002-20001*) disclosed a

[denial-of-service attack](https://en.wikipedia.org/wiki/Denial-of-service_attack)(DoS) against the protocol variants using ephemeral keys, called D(HE)at attack.

The attack exploits that the Diffie–Hellman key exchange allows attackers to send arbitrary numbers that are actually not public keys, triggering expensive modular exponentiation calculations on the victim's side. Another CVEs release disclosed that the Diffie–Hellman key exchange implementations may use long private exponents (

[[19]](https://en.wikipedia.org#cite_note-dheatattack-20)*) that arguably make modular exponentiation calculations unnecessarily expensive*

[CVE-2022-40735](https://nvd.nist.gov/vuln/detail/CVE-2022-40735)or may unnecessarily check a peer's public key (

[[20]](https://en.wikipedia.org#cite_note-Oorschot_Wiener_1996-21)*) which has similar resource requirement as key calculation using a long exponent.*

[CVE-2024-41996](https://nvd.nist.gov/vuln/detail/CVE-2024-41996)An attacker can exploit both vulnerabilities together.

[[21]](https://en.wikipedia.org#cite_note-22)### Practical attacks on Internet traffic

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=13)]

The [number field sieve](https://en.wikipedia.org/wiki/General_number_field_sieve) algorithm, which is generally the most effective in solving the [discrete logarithm problem](https://en.wikipedia.org/wiki/Discrete_logarithm_problem), consists of four computational steps. The first three steps only depend on the order of the group G, not on the specific number whose finite log is desired. [22] It turns out that much Internet traffic uses one of a handful of groups that are of order 1024 bits or less.

By

[[2]](https://en.wikipedia.org#cite_note-imperfectfs-3)[precomputing](https://en.wikipedia.org/wiki/Precomputing)the first three steps of the number field sieve for the most common groups, an attacker need only carry out the last step, which is much less computationally expensive than the first three steps, to obtain a specific logarithm. The

[Logjam](https://en.wikipedia.org/wiki/Logjam_(computer_security))attack used this vulnerability to compromise a variety of Internet services that allowed the use of groups whose order was a 512-bit prime number, so called

[export grade](https://en.wikipedia.org/wiki/Export_of_cryptography). The authors needed several thousand CPU cores for a week to precompute data for a single 512-bit prime. Once that was done, individual logarithms could be solved in about a minute using two 18-core Intel Xeon CPUs.

[[2]](https://en.wikipedia.org#cite_note-imperfectfs-3)As estimated by the authors behind the Logjam attack, the much more difficult precomputation needed to solve the discrete log problem for a 1024-bit prime would cost on the order of $100 million, well within the budget of a large national [intelligence agency](https://en.wikipedia.org/wiki/Intelligence_agency) such as the U.S. [National Security Agency](https://en.wikipedia.org/wiki/National_Security_Agency) (NSA). The Logjam authors speculate that precomputation against widely reused 1024-bit DH primes is behind claims in [leaked NSA documents](https://en.wikipedia.org/wiki/2010s_global_surveillance_disclosures) that NSA is able to break much of current cryptography.[[2]](https://en.wikipedia.org#cite_note-imperfectfs-3)

To avoid these vulnerabilities, the Logjam authors recommend use of [elliptic curve cryptography](https://en.wikipedia.org/wiki/Elliptic_curve_cryptography), for which no similar attack is known. Failing that, they recommend that the order, *p*, of the Diffie–Hellman group should be at least 2048 bits. They estimate that the pre-computation required for a 2048-bit prime is 109 times more difficult than for 1024-bit primes.[[2]](https://en.wikipedia.org#cite_note-imperfectfs-3)

### Security against quantum computers

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=14)]

[Quantum computers](https://en.wikipedia.org/wiki/Quantum_computing) can break public-key cryptographic schemes, such as RSA, finite-field DH and elliptic-curve DH key-exchange protocols, using [Shor's algorithm](https://en.wikipedia.org/wiki/Shor%27s_algorithm) for solving the [factoring problem](https://en.wikipedia.org/wiki/Integer_factorization), the [discrete logarithm problem](https://en.wikipedia.org/wiki/Discrete_logarithm), and the period-finding problem. A [post-quantum variant of Diffie-Hellman algorithm](https://en.wikipedia.org/wiki/Post-Quantum_Extended_Diffie%E2%80%93Hellman) was proposed in 2023, and relies on a combination of the quantum-resistant CRYSTALS-Kyber protocol, as well as the old elliptic curve [X25519](https://en.wikipedia.org/wiki/X25519) protocol.

## Other uses

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=15)]

### Encryption

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=16)]

Public key encryption schemes based on the Diffie–Hellman key exchange have been proposed. The first such scheme is the [ElGamal encryption](https://en.wikipedia.org/wiki/ElGamal_encryption). A more modern variant is the [Integrated Encryption Scheme](https://en.wikipedia.org/wiki/Integrated_Encryption_Scheme).

### Forward secrecy

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=17)]

Protocols that achieve [forward secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) generate new key pairs for each [session](https://en.wikipedia.org/wiki/Session_(computer_science)) and discard them at the end of the session. The Diffie–Hellman key exchange is a frequent choice for such protocols, because of its fast key generation.

### Password-authenticated key agreement

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=18)]

When Alice and Bob share a password, they may use a [password-authenticated key agreement](https://en.wikipedia.org/wiki/Password-authenticated_key_agreement) (PK) form of Diffie–Hellman to prevent man-in-the-middle attacks. One simple scheme is to compare the [hash](https://en.wikipedia.org/wiki/Cryptographic_hash_function) of **s** concatenated with the password calculated independently on both ends of channel. A feature of these schemes is that an attacker can only test one specific password on each iteration with the other party, and so the system provides good security with relatively weak passwords. This approach is described in [ITU-T](https://en.wikipedia.org/wiki/ITU-T) Recommendation [X.1035](https://en.wikipedia.org/wiki/X.1035), which is used by the [G.hn](https://en.wikipedia.org/wiki/G.hn) home networking standard.

An example of such a protocol is the [Secure Remote Password protocol](https://en.wikipedia.org/wiki/Secure_Remote_Password_protocol).

### Public key

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=19)]

It is also possible to use Diffie–Hellman as part of a [public key infrastructure](https://en.wikipedia.org/wiki/Public_key_infrastructure), allowing Bob to encrypt a message so that only Alice will be able to decrypt it, with no prior communication between them other than Bob having trusted knowledge of Alice's public key. Alice's public key is . To send her a message, Bob chooses a random *b* and then sends Alice (unencrypted) together with the message encrypted with symmetric key . Only Alice can determine the symmetric key and hence decrypt the message because only she has *a* (the private key). A pre-shared public key also prevents man-in-the-middle attacks.

In practice, Diffie–Hellman is not used in this way, with [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) being the dominant public key algorithm. This is largely for historical and commercial reasons,[ namely that

[citation needed](https://en.wikipedia.org/wiki/Wikipedia:Citation_needed)]

[RSA Security](https://en.wikipedia.org/wiki/RSA_(security_firm))created a

[certificate authority](https://en.wikipedia.org/wiki/Certificate_authority)for key signing that became

[Verisign](https://en.wikipedia.org/wiki/Verisign). Diffie–Hellman, as elaborated above, cannot directly be used to sign certificates. However, the

[ElGamal](https://en.wikipedia.org/wiki/ElGamal_signature_scheme)and

[DSA](https://en.wikipedia.org/wiki/Digital_Signature_Algorithm)signature algorithms are mathematically related to it, as well as

[MQV](https://en.wikipedia.org/wiki/MQV),

[STS](https://en.wikipedia.org/wiki/Station-to-Station_protocol)and the

[IKE](https://en.wikipedia.org/wiki/Internet_Key_Exchange)component of the

[IPsec](https://en.wikipedia.org/wiki/IPsec)protocol suite for securing

[Internet Protocol](https://en.wikipedia.org/wiki/Internet_Protocol)communications.

## See also

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=20)]

[Elliptic-curve Diffie–Hellman](https://en.wikipedia.org/wiki/Elliptic-curve_Diffie%E2%80%93Hellman)key exchange[Supersingular isogeny key exchange](https://en.wikipedia.org/wiki/Supersingular_isogeny_key_exchange)[Forward secrecy](https://en.wikipedia.org/wiki/Forward_secrecy)[Diffie–Hellman problem](https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_problem)[Modular exponentiation](https://en.wikipedia.org/wiki/Modular_exponentiation)[Denial-of-service attack](https://en.wikipedia.org/wiki/Denial-of-service_attack)[Post-Quantum Extended Diffie–Hellman](https://en.wikipedia.org/wiki/Post-Quantum_Extended_Diffie%E2%80%93Hellman)[Accumulator (cryptography)](https://en.wikipedia.org/wiki/Accumulator_(cryptography))

## Notes

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=21)]

Synonyms of Diffie–Hellman key exchange include:[^](https://en.wikipedia.org#cite_ref-1)- Diffie–Hellman–Merkle key exchange
- Diffie–Hellman key agreement
- Diffie–Hellman key establishment
- Diffie–Hellman key negotiation
- Exponential key exchange
- Diffie–Hellman protocol
- Diffie–Hellman handshake

## References

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=22)]

Merkle, Ralph C. (April 1978). "Secure Communications Over Insecure Channels".[^](https://en.wikipedia.org#cite_ref-Merkle_1978_2-0).[Communications of the ACM](https://en.wikipedia.org/wiki/Communications_of_the_ACM)**21**(4): 294–299.[CiteSeerX](https://en.wikipedia.org/wiki/CiteSeerX_(identifier))[10.1.1.364.5157](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.364.5157).[doi](https://en.wikipedia.org/wiki/Doi_(identifier)):[10.1145/359460.359473](https://doi.org/10.1145%2F359460.359473).[S2CID](https://en.wikipedia.org/wiki/S2CID_(identifier))[6967714](https://api.semanticscholar.org/CorpusID:6967714).Received August, 1975; revised September 1977

- ^
**a****b****c****d****e**Adrian, David; et al. (October 2015).**f**["Imperfect Forward Secrecy: How Diffie–Hellman Fails in Practice"](https://weakdh.org/imperfect-forward-secrecy-ccs15.pdf)(PDF).[Archived](https://web.archive.org/web/20150906213656/https://weakdh.org/imperfect-forward-secrecy-ccs15.pdf)(PDF) from the original on 2015-09-06. - ^
**a****b**[Diffie, Whitfield](https://en.wikipedia.org/wiki/Whitfield_Diffie);[Hellman, Martin E.](https://en.wikipedia.org/wiki/Martin_Hellman)(November 1976).["New Directions in Cryptography"](http://ee.stanford.edu/%7Ehellman/publications/24.pdf)(PDF)..[IEEE Transactions on Information Theory](https://en.wikipedia.org/wiki/IEEE_Transactions_on_Information_Theory)**22**(6): 644–654.[Bibcode](https://en.wikipedia.org/wiki/Bibcode_(identifier)):[1976ITIT...22..644D](https://ui.adsabs.harvard.edu/abs/1976ITIT...22..644D).[CiteSeerX](https://en.wikipedia.org/wiki/CiteSeerX_(identifier))[10.1.1.37.9720](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.37.9720).[doi](https://en.wikipedia.org/wiki/Doi_(identifier)):[10.1109/TIT.1976.1055638](https://doi.org/10.1109%2FTIT.1976.1055638).[Archived](https://web.archive.org/web/20141129035850/https://ee.stanford.edu/%7Ehellman/publications/24.pdf)(PDF) from the original on 2014-11-29. [^](https://en.wikipedia.org#cite_ref-5)[Ellis, J. H.](https://en.wikipedia.org/wiki/James_H._Ellis)(January 1970).["The possibility of Non-Secret digital encryption"](https://web.archive.org/web/20141030210530/https://cryptocellar.web.cern.ch/cryptocellar/cesg/possnse.pdf)(PDF).*CESG Research Report*. Archived from[the original](http://cryptocellar.web.cern.ch/cryptocellar/cesg/possnse.pdf)(PDF) on 2014-10-30. Retrieved 2015-08-28.[^](https://en.wikipedia.org#cite_ref-6)["The Possibility of Secure Secret Digital Encryption"](https://www.gchq.gov.uk/sites/default/files/document_files/CESG_Research_Report_No_3006_0.pdf)(PDF).[Archived](https://web.archive.org/web/20170216051636/https://www.gchq.gov.uk/sites/default/files/document_files/CESG_Research_Report_No_3006_0.pdf)(PDF) from the original on 2017-02-16. Retrieved 2017-07-08.[^](https://en.wikipedia.org#cite_ref-7)["GCHQ trio recognised for key to secure shopping online"](https://www.bbc.co.uk/news/uk-england-gloucestershire-11475101).. 5 October 2010.[BBC News](https://en.wikipedia.org/wiki/BBC_News)[Archived](https://web.archive.org/web/20140810044800/http://www.bbc.co.uk/news/uk-england-gloucestershire-11475101)from the original on 10 August 2014. Retrieved 5 August 2014.[^](https://en.wikipedia.org#cite_ref-8)[US patent 4200770](https://worldwide.espacenet.com/textdoc?DB=EPODOC&IDX=US4200770)Hellman, Martin E. (May 2002),[^](https://en.wikipedia.org#cite_ref-Hellman2002_9-0)["An overview of public key cryptography"](http://www-ee.stanford.edu/~hellman/publications/31.pdf)(PDF),*IEEE Communications Magazine*,**40**(5): 42–49,[Bibcode](https://en.wikipedia.org/wiki/Bibcode_(identifier)):[2002IComM..40e..42H](https://ui.adsabs.harvard.edu/abs/2002IComM..40e..42H),[CiteSeerX](https://en.wikipedia.org/wiki/CiteSeerX_(identifier))[10.1.1.127.2652](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.127.2652),[doi](https://en.wikipedia.org/wiki/Doi_(identifier)):[10.1109/MCOM.2002.1006971](https://doi.org/10.1109%2FMCOM.2002.1006971),[S2CID](https://en.wikipedia.org/wiki/S2CID_(identifier))[9504647](https://api.semanticscholar.org/CorpusID:9504647),[archived](https://web.archive.org/web/20160402093741/http://www-ee.stanford.edu/%7Ehellman/publications/31.pdf)(PDF) from the original on 2016-04-02Wong, David (2021). "Key exchange standards".[^](https://en.wikipedia.org#cite_ref-10). Manning.*Real World Cryptography*[ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier))[9781617296710](https://en.wikipedia.org/wiki/Special:BookSources/9781617296710)– via Google Books.`{{`

: CS1 maint: deprecated archival service ([cite book](https://en.wikipedia.org/wiki/Template:Cite_book)}}[link](https://en.wikipedia.org/wiki/Category:CS1_maint:_deprecated_archival_service))Buchmann, Johannes A. (2013).[^](https://en.wikipedia.org#cite_ref-11)(Second ed.). Springer Science+Business Media. pp. 190–191.*Introduction to Cryptography*[ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier))[978-1-4419-9003-7](https://en.wikipedia.org/wiki/Special:BookSources/978-1-4419-9003-7).Castryck, Wouter; Decru, Thomas (April 2023).[^](https://en.wikipedia.org#cite_ref-castryckdecru2023_12-0)["An efficient key recovery attack on SIDH"](https://web.archive.org/web/20240926174200/https://eprint.iacr.org/2022/975.pdf)(PDF).*Annual International Conference on the Theory and Applications of Cryptographic Techniques*: 423–447. Archived from[the original](https://eprint.iacr.org/2022/975.pdf)(PDF) on 2024-09-26.Barker, Elaine; Chen, Lily; Roginsky, Allen; Vassilev, Apostol; Davis, Richard (2018-04-16).[^](https://en.wikipedia.org#cite_ref-13)[Recommendation for Pair-Wise Key-Establishment Schemes Using Discrete Logarithm Cryptography](https://csrc.nist.gov/Pubs/sp/800/56/a/r3/Final)(Report). National Institute of Standards and Technology.Blake-Wilson, Simon; Johnson, Don; Menezes, Alfred (1997), "Key Agreement Protocols and their Security Analysis",[^](https://en.wikipedia.org#cite_ref-14)*Crytography and Coding*, Lecture Notes in Computer Science, vol. 1355, pp. 30–45,[CiteSeerX](https://en.wikipedia.org/wiki/CiteSeerX_(identifier))[10.1.1.25.387](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.25.387),[doi](https://en.wikipedia.org/wiki/Doi_(identifier)):[10.1007/BFb0024447](https://doi.org/10.1007%2FBFb0024447),[ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier))[978-3-540-63927-5](https://en.wikipedia.org/wiki/Special:BookSources/978-3-540-63927-5)Kudla, Caroline; Paterson, Kenneth G. (2005). "Modular Security Proofs for Key Agreement Protocols". In Roy, Bimal (ed.).[^](https://en.wikipedia.org#cite_ref-15)(PDF). Lecture Notes in Computer Science. Vol. 3788. Berlin, Heidelberg: Springer. pp. 549–565.*Advances in Cryptology - ASIACRYPT 2005*[doi](https://en.wikipedia.org/wiki/Doi_(identifier)):[10.1007/11593447_30](https://doi.org/10.1007%2F11593447_30).[ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier))[978-3-540-32267-2](https://en.wikipedia.org/wiki/Special:BookSources/978-3-540-32267-2).[^](https://en.wikipedia.org#cite_ref-16)[US11025421B2](https://patents.google.com/patent/US11025421B2/en?oq=11025421), Fay, Bjorn, "Advanced modular handshake for key agreement and optional authentication", issued 2021-06-01- ^
**a****b****c****d**["Specifications >> The X3DH Key Agreement Protocol"](https://www.signal.org/docs/specifications/x3dh/).*Signal Messenger*. Barbulescu, Razvan; Gaudry, Pierrick; Joux, Antoine; Thomé, Emmanuel (2014).[^](https://en.wikipedia.org#cite_ref-18)["A Heuristic Quasi-Polynomial Algorithm for Discrete Logarithm in Finite Fields of Small Characteristic"](http://hal.inria.fr/docs/00/90/90/87/PDF/article.pdf)(PDF).*Advances in Cryptology – EUROCRYPT 2014*. Proceedings 33rd Annual International Conference on the Theory and Applications of Cryptographic Techniques. Lecture Notes in Computer Science. Vol. 8441. Copenhagen, Denmark. pp. 1–16.[doi](https://en.wikipedia.org/wiki/Doi_(identifier)):[10.1007/978-3-642-55220-5_1](https://doi.org/10.1007%2F978-3-642-55220-5_1).[ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier))[978-3-642-55220-5](https://en.wikipedia.org/wiki/Special:BookSources/978-3-642-55220-5).[Archived](https://web.archive.org/web/20200322030320/https://hal.inria.fr/docs/00/90/90/87/PDF/article.pdf)(PDF) from the original on 2020-03-22."RFC 4306 Internet Key Exchange (IKEv2) Protocol". Internet Engineeringrg/web/20150107073645/[^](https://en.wikipedia.org#cite_ref-19)[http://www.ietf.org/rfc/rfc4306.txt](http://www.ietf.org/rfc/rfc4306.txt).Pfeiffer, Szilárd; Tihanyi, Norbert (25 December 2023).[^](https://en.wikipedia.org#cite_ref-dheatattack_20-0)["D(HE)at: A Practical Denial-of-Service Attack on the Finite Field Diffie-Hellman Key Exchange"](https://doi.org/10.1109%2FACCESS.2023.3347422)..[IEEE Access](https://en.wikipedia.org/wiki/IEEE_Access)**12**: 957–980.[doi](https://en.wikipedia.org/wiki/Doi_(identifier)):[10.1109/ACCESS.2023.3347422](https://doi.org/10.1109%2FACCESS.2023.3347422).van Oorschot, P.C.; Wiener, M.J. (1996).[^](https://en.wikipedia.org#cite_ref-Oorschot_Wiener_1996_21-0)["On Diffie-Hellman Key Agreement with Short Exponents"](https://link.springer.com/chapter/10.1007/3-540-68339-9_29).*Advances in Cryptology — EUROCRYPT '96*. Lecture Notes in Computer Science. Vol. 1070. Springer, Berlin, Heidelberg (published 2001). pp. 332–343.[doi](https://en.wikipedia.org/wiki/Doi_(identifier)):[10.1007/3-540-68339-9_29](https://doi.org/10.1007%2F3-540-68339-9_29).[ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier))[978-3-540-61186-8](https://en.wikipedia.org/wiki/Special:BookSources/978-3-540-61186-8).[Archived](https://web.archive.org/web/20230219191210/https://link.springer.com/chapter/10.1007/3-540-68339-9_29)from the original on 2023-02-19.Elaine, Barker; Lily, Chen; Allen, Roginsky; Apostol, Vassilev; Richard, Davis (2018).[^](https://en.wikipedia.org#cite_ref-22)["Recommendation for Pair-Wise Key-Establishment Schemes Using Discrete Logarithm Cryptography"](https://csrc.nist.gov/pubs/sp/800/56/a/r3/final). National Institute of Standards and Technology.[doi](https://en.wikipedia.org/wiki/Doi_(identifier)):[10.6028/NIST.SP.800-56Ar3](https://doi.org/10.6028%2FNIST.SP.800-56Ar3).Whitfield Diffie, Paul C. Van Oorschot, and Michael J. Wiener "Authentication and Authenticated Key Exchanges", in Designs, Codes and Cryptography, 2, 107–125 (1992), Section 5.2, available as Appendix B to[^](https://en.wikipedia.org#cite_ref-23)[U.S. patent 5,724,425](https://patents.google.com/patent/US5724425)

### General references

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=23)]

- Gollman, Dieter (2011).
*Computer Security*(2nd ed.). West Sussex, England: John Wiley & Sons, Ltd.[ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier))[978-0470741153](https://en.wikipedia.org/wiki/Special:BookSources/978-0470741153). - Williamson, Malcolm J. (January 21, 1974).
(PDF) (Technical report). Communications Electronics Security Group.*Non-secret encryption using a finite field*[Archived](https://web.archive.org/web/20170323052715/https://www.gchq.gov.uk/sites/default/files/document_files/nonsecret_encryption_finite_field_0.pdf)(PDF) from the original on 2017-03-23. Retrieved 2017-03-22. - Williamson, Malcolm J. (August 10, 1976).
(PDF) (Technical report). Communications Electronics Security Group.*Thoughts on Cheaper Non-Secret Encryption*[Archived](https://web.archive.org/web/20040719085349/http://www.fi.muni.cz/usr/matyas/lecture/paper3.pdf)(PDF) from the original on 2004-07-19. Retrieved 2015-08-25. [The History of Non-Secret Encryption](https://web.archive.org/web/20130404174201/https://cryptocellar.web.cern.ch/cryptocellar/cesg/ellis.pdf)[JH Ellis](https://en.wikipedia.org/wiki/James_H._Ellis)1987 (28K PDF file) ([HTML version](https://web.archive.org/web/20040808040209/http://jya.com/ellisdoc.htm))[The First Ten Years of Public-Key Cryptography](http://cr.yp.to/bib/1988/diffie.pdf)Whitfield Diffie, Proceedings of the IEEE, vol. 76, no. 5, May 1988, pp: 560–577 (1.9MB PDF file)[Menezes, Alfred](https://en.wikipedia.org/wiki/Alfred_Menezes);[van Oorschot, Paul](https://en.wikipedia.org/wiki/Paul_van_Oorschot);[Vanstone, Scott](https://en.wikipedia.org/wiki/Scott_Vanstone)(1997).Boca Raton, Florida: CRC Press.[Handbook of Applied Cryptography](https://en.wikipedia.org/w/index.php?title=Handbook_of_Applied_Cryptography&action=edit&redlink=1)[ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier))[0-8493-8523-7](https://en.wikipedia.org/wiki/Special:BookSources/0-8493-8523-7). ([Available online](http://www.cacr.math.uwaterloo.ca/hac/))[Singh, Simon](https://en.wikipedia.org/wiki/Simon_Singh)(1999)New York: Doubleday[The Code Book: the evolution of secrecy from Mary Queen of Scots to quantum cryptography](https://en.wikipedia.org/wiki/The_Code_Book:_the_evolution_of_secrecy_from_Mary_Queen_of_Scots_to_quantum_cryptography)[ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier))[0-385-49531-5](https://en.wikipedia.org/wiki/Special:BookSources/0-385-49531-5)[An Overview of Public Key Cryptography](https://dx.doi.org/10.1109/MCOM.2002.1006971)Martin E. Hellman, IEEE Communications Magazine, May 2002, pp. 42–49. (123kB PDF file)

## External links

[[edit](https://en.wikipedia.org/w/index.php?title=Diffie%E2%80%93Hellman_key_exchange&action=edit§ion=24)]

[Oral history interview with Martin Hellman](https://conservancy.umn.edu/handle/11299/107353),[Charles Babbage Institute](https://en.wikipedia.org/wiki/Charles_Babbage_Institute), University of Minnesota. Leading cryptography scholar Martin Hellman discusses the circumstances and fundamental insights of his invention of public key cryptography with collaborators Whitfield Diffie and Ralph Merkle at[Stanford University](https://en.wikipedia.org/wiki/Stanford_University)in the mid-1970s.- RFC
[2631](https://www.rfc-editor.org/rfc/rfc2631)–*Diffie–Hellman Key Agreement Method*. E. Rescorla. June 1999. - RFC
[3526](https://www.rfc-editor.org/rfc/rfc3526)–*More Modular Exponential (MODP) Diffie–Hellman groups for Internet Key Exchange (IKE)*. T. Kivinen, M. Kojo, SSH Communications Security. May 2003.
