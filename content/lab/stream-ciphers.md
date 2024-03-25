+++
title = "Stream Ciphers"
description = "Visual explanation of stream cipher algorithms."
date = 2025-01-05
draft = true
template = "article.html"
[extra]
type = "article"
thumbnail = "lab.bits.svg"
thumbnailalt = "Small lines of rectangles representing bits."
+++

Encryption is a way to encode data so that only people who have 'keys' to the encoded data can 'unlock' or decrypt it. There are different ways to encrypt data, but most can be classified into two main categories based on the type of keys used.

The first kind employs one key to both encrypt and decrypt data, and is called [symmetric key cryptography](https://en.wikipedia.org/wiki/Symmetric-key_algorithm) — due to the symmetry of keys involved in the encryption-decryption process. The second type, called [asymmetric key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography), involves using a key to encrypt the data and a separate key to decrypt the encrypted data.

This post is primarily about symmetric key cryptography, and more specifically about stream ciphers.

## Caesar Cipher

One of the simplest encryption techniques includes the [Caesar cipher](https://en.wikipedia.org/wiki/Caesar_cipher), a type of [simple substitution cipher](https://en.wikipedia.org/wiki/Substitution_cipher#Simple). The message to be encrypted (called plaintext) is encoded by substituting its letters with the corresponding letters from an alphabet that is 'shifted' or 'rotated' to the left or right by some amount:

{{ loadData(path="/static/media/lab/stream-ciphers/caesar-encryption.txt") }}

If the letters are encoded as a number determined by its position in the alphabet, then the encrypted letter for a plaintext letter `m` is `E(m) = (m + k) mod 26`, where `k` is the shift value. The encrypted message is often referred to as the ciphertext. Decryption has to reverse the encryption operation. So the decrypted letter for the ciphertext letter `c` is then `D(c) = (c - k) mod 26`.

{{ loadData(path="/static/media/lab/stream-ciphers/caesar-decryption.txt") }}

{% tangent(summary="Modulo Operation", open=true) %}
The `mod` or [modulo operator](https://en.wikipedia.org/wiki/Modulo) returns the remainder after division by a number — which in this case is 26, the number of letters in the Latin alphabet.
{% end %}

The [ROT13](https://en.wikipedia.org/wiki/ROT13) is a popular and special case of a Caesar cipher, having a shift value of 13. Since the Latin alphabet has 26 letters, shifting the alphabet to the left by 13 positions is the same as shifting it to the right by 13 positions. So, decryption can be defined as the same operation as encryption. That is, for a plaintext message `m` with ciphertext `c`:

`E(m) = (m + 13) mod 26 = (m - 13) mod 26 = c`\
`D(c) = (c + 13) mod 26 = (c - 13) mod 26 = m`

Both the encryption and decryption operations are the same. The only difference is the domain of the operators — one operates on the plaintext while the other operates on the ciphertext — but that difference is purely semantical.

{{ loadData(path="/static/media/lab/stream-ciphers/caesar-rot13.txt") }}

The shift parameter in the Caesar cipher determines how a message gets encrypted and decrypted — it acts as a 'key' for encrypting and decrypting the data. Only parties who have the knowledge about the keys can decrypt the messages encrypted with that key. While this is the main goal of symmetric encryption, the Caesar cipher is not a very good way to achieve this goal.

Single-alphabet substitution ciphers like the Caesar cipher are not at all secure, and they can be very easily broken — since [brute forcing](https://en.wikipedia.org/wiki/Brute-force_attack) all possible keys takes a trivial amount of time. It can alternatively also be broken by trying to [match the frequency distribution](https://en.wikipedia.org/wiki/Frequency_analysis#Frequency_analysis_for_simple_substitution_ciphers) of letters of the ciphertext and the frequency distribution of letters of a language.

{% tangent(summary="Brute force attacks", open=true) %}
A brute force attack refers to systematically trying all possible combinations of a secret key or password, until the correct one is found.
{% end %}

## One-Time Pad

In the Caesar cipher all the letters are shifted by the same amount, determined by a single-valued key. However, employing separate shift values for each letter is arguably more secure. The [Vigenère cipher](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher) is a [polyalphabetic substitution ciper](https://en.wikipedia.org/wiki/Polyalphabetic_cipher) — it uses a key with multiple shift values for encrypting messages. If the key is shorter than the plaintext message, the key is repeated until it matches the length of the message.

{{ loadData(path="/static/media/lab/stream-ciphers/vigenere-encryption.txt") }}

Again, decryption involves subtracting the key from the ciphertext using modular artihmetic:

{{ loadData(path="/static/media/lab/stream-ciphers/vigenere-decryption.txt") }}

Although more secure than the Caesar cipher, the Vigenère cipher is [not secure](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher#Cryptanalysis) because of the repeating nature of the key. If length of a key is correctly guessed, the ciphertext can be treated as interweaved Caesar ciphers — all of which can be individually broken rather trivially.

{{ loadData(path="/static/media/lab/stream-ciphers/vigenere-break.txt") }}

Using a key which is at least as long as the plaintext, and where each shift value is [truly random](https://en.wikipedia.org/wiki/Random_number_generation#True_vs._pseudo-random_numbers) will be [perfectly secure](https://en.wikipedia.org/wiki/Information-theoretic_security) — as long as the key is kept secret, and is **never** reused.

{{ loadData(path="/static/media/lab/stream-ciphers/one-time-pad-encryption-decryption.txt") }}

This cipher scheme, involving a truly random key that is as long as the plaintext is called the [one-time pad](https://en.wikipedia.org/wiki/One-time_pad). The only information that is leaked is the maximum possible length of the message. However as mentioned, the moment the same key is used more than once, its security benefits vanish. And hence the name.

To understand why reusing keys is dangerous, consider two different messages that are encrypted with the same key. Attackers can subtract the ciphertext of one message from the other to leak data about the plaintext. For example, if `m1` and `m2` are messages that are both encrypted with key `k` then:

`c1 = (m1 + k) mod 26`\
`c2 = (m2 + k) mod 26`

Subtracting ciphertext `c1` from `c2` eliminates `k` and reveals `m2 - m1 (mod 26)`. Attackers can use this information to break the cipher.

{{ loadData(path="/static/media/lab/stream-ciphers/one-time-pad-break.txt") }}

{% tangent(summary="Visualising plaintext leakage", open=true) %}
This is an example of how difference in ciphertexts can leak information. Two grayscale images are both encrypted with the same key. An attacker can subtract one encrypted image from the other, exposing information about the original images.
{% end %}

## Vernam Cipher

Reducing the modulus of the one-time pad can make harware implementations easier. The [Vernam cipher](https://en.wikipedia.org/wiki/Gilbert_Vernam#The_Vernam_cipher) is a type of one-time pad that uses modulo two arithmetic. That is:

`c = (m + k) mod 2`\
`m = (c - k) mod 2`

Where `c` is the ciphertext for the binary plaintext message `m` encrypted using binary key `k`. Since the result of `n mod 2` is either zero or one, `c` is also binary. Addition and subtraction in modulo two arithmetic is the [same](https://en.wikipedia.org/wiki/GF(2)#Properties), so like ROT13, the same operation can be used for encryption and decryption:

`c = (m + k) mod 2`\
`m = (c + k) mod 2`

{{ loadData(path="/static/media/lab/stream-ciphers/vernam-encryption-decryption.txt") }}

Modulo two addition is implemented in hardware using [XOR gates](https://en.wikipedia.org/wiki/XOR_gate). So the ciphertext can be generated by combining a plaintext message with a key using the XOR operator:

`c = (m + k) mod 2 = m ⊕ k`\
`m = (c + k) mod 2 = c ⊕ k`

{{ loadData(path="/static/media/lab/stream-ciphers/vernam-encryption-decryption-xor.txt") }}

{% tangent(summary="The XOR operation", open=true) %}
The [XOR operator](https://en.wikipedia.org/wiki/Exclusive_or) `⊕` takes two binary inputs and returns one if and only if one of the inputs is one, otherwise it returns zero — same as modulo two addtion using binary numbers.
{% end %}

The binary key of the Vernam cipher is often referred to as a keystream, since it can be viewed as a stream of bits that is XOR-ed bitwise with the stream of plaintext bits to generate the ciphertext stream.

The Vernam cipher keystream must have the same properties as the one-time pad to be secure. It should be at least as long as the plaintext stream, and should be truly random. And again, the key should never be reused, as otherwise it can leak information about the plaintext:

{{ loadData(path="/static/media/lab/stream-ciphers/vernam-break.txt") }}

{% tangent(summary="XOR self inverse", open=true) %}
In XOR, a number is its own inverse. That is `x ⊕ x = 0` and `y ⊕ x ⊕ x` = `y ⊕ 0` = `y`. The XOR operations are also [associative](https://en.wikipedia.org/wiki/Associative_property) and [commutative](https://en.wikipedia.org/wiki/Commutative_property). These properties can be exploited to leak plaintext data by XOR-ing two ciphertexts encrypted with the same key:

`c1 ⊕ c2`\
`= (m1 ⊕ k) ⊕ (m2 ⊕ k)`\
`= m1 ⊕ k ⊕ m2 ⊕ k`\
`= m1 ⊕ m2 ⊕ k ⊕ k`\
`= m1 ⊕ m2`
{% end %}

## ChaCha20 Cipher

Even though the Vernam cipher allows for easy encryption and decryption of data using computer hardware and is perfectly secure, it still relies on secure and secret distribution of keys, which is often impractical. If a key (which is at least the size of the message) can be securely transmitted, it makes more sense to simply send the message itself instead.

A simpler approach for exchanging keys is for the communicating parties to have a sort of a random number generator that somehow generates the **same** random keystream for both parties. Such random number generators [do exist](https://en.wikipedia.org/wiki/Pseudorandom_number_generator). Most of them generate numbers that *appear* random from an initial value called the seed. For the same seed value, the same stream of random numbers is generated.

Communicating parties can then encrypt and decrypt messages by securely the seed values, and then encrypt and decrypt data using the random keystream generated by the random number generator.

{{ loadData(path="/static/media/lab/stream-ciphers/prf-stream.txt") }}

However, there are caveats to this. Since the keystream is completely determined by the seed, it is not truly random and thefore not perfectly secure. But while it is not *perfectly* secure, it is still *reasonably* secure — as long as an attacker cannot easily recreate the original keystream.

One way to generate such pseudorandom keystreams is using ARX (add-rotate-XOR) operations on a seed value. The [ChaCha20](https://en.wikipedia.org/wiki/Salsa20#ChaCha_variant) cipher is an example of an [ARX cipher](https://en.wikipedia.org/wiki/Block_cipher#ARX_(add%E2%80%93rotate%E2%80%93XOR)) that uses a 512-bit value as its seed.

### ARX Operations

ChaCha20 generates a pseudorandom keystream from a 512-bit block by first dividing it into a 4x4 block of 32-bit [words](https://en.wikipedia.org/wiki/Word_(computer_architecture)).

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-words-init.txt") }}

A pseudorandom block is generated from this block by performing addition, rotation and XOR operations on the words. The ARX operations can be grouped into rounds, and each round can be divided into four quarter rounds. A quarter round operates on four words at a time, and is defined as:

`a += b; d ^= a; d <<<= 16;`\
`c += d; b ^= c; b <<<= 12;`\
`a += b; d ^= a; d <<<=  8;`\
`c += d; b ^= c; b <<<=  7;`

These operations effectively 'mix' or [diffuse](https://cr.yp.to/snuffle/diffusion.html) the bits of the four words with each other:

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-diffusion-operations.txt") }}

Performing the quarter rounds four times makes up one full round. On odd rounds, the quarter round is performed on all four columns of the matrix, while on even rounds, the quarter rounds is performed on the four left diagonals of the matrix. ChaCha20 specifies performing a total of twenty rounds, or ten odd rounds and ten even rounds.

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-diffusion-rounds.txt") }}

Performing all the twenty rounds generates a pseudorandom 512-bit block. However it is not the part of the final keystream. The diffused block is first added to the original block before it forms a part of the keystream.

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-diffusion-addition.txt") }}

The addition step is important since the mixing rounds are invertible — without adding it to the original block, it is possible to apply the reverse operations on the pseudorandom block to produce the original block.

### Counter & Nonce

The above operations generate a pseudorandom 512-bit block from a 512-bit seed block. This pseudorandom block can be XOR-ed with a 512-bit plaintext stream to produce the ciphertext.

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-xor.txt") }}

However to encrypt longer messages, more pseudorandom blocks are required. The blocks must not repeat and must be different from each other for them to be considered secure — or else an attacker can use the same techniques used to break the Vigenère cipher to break ChaCha20.

Producing more blocks which are different from the generated block using the same ARX operations on the same seed block is however, impossible. Since the ARX operations are deterministic, the same seed block always produces the same pseudorandom block. The only way to generate different blocks is to alter the operations, or alter the seed block.

Having a standard way to alter the initial state block is much cleaner than having altering operations for each block. Altering the initial state block can involve simply changing just a few bits — due to the cascading effects of diffusion, even a single bit flip results in a completely different pseudorandom block.

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-diffusion-avalanche.txt") }}

In ChaCha20, the last four words (128 bits) are reserved in the original 512-bit block for the sole purpose of generating new blocks. The four words are logically separated into two parts — a counter and a nonce.

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-words-seed.txt") }}

To encrypt longer messages, the counter gets incremented — and the the bit flips result in the creation of new, different blocks. Two words (64 bits) are assigned for the counter in ChaCha20. So, there can be 2^64 new blocks, each of size 512-bits. Thus, plaintext data of size of up to 1 ZiB can be encrypted using the keystream.

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-counter-increment.txt") }}

However, if the counter is reset to zero when sending a new message, and the counter values repeat — the output pseudorandom blocks will also repeat:

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-counter-reset.txt") }}

Encrypting data using reused keystreams (blocks) is dangerous. So the counter values must never repeat, and must always be incrementing. But this is not ideal. If any part of some message needs to be encrypted (or decrypted) again, it would require finding its corresponding counter value. The counter value is not just its position in the message — it would also need to take into account the the ordinal value of the message itself.

A cleaner approach to prevent repeating blocks, is by using a nonce. A nonce is simply a number used once. Whenever a new message needs to be encrypted a new and unique nonce is generated. This ensures the entire initial state block is always unique even if the counter values are not. And, since counters can repeat, they can then be used to truly represent positional information.

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-counter-reset-new-nonce.txt") }}

The nonce is also two words (64 bits). So theoretically, a total of 2^64 messages, each of size 1 ZiB can be encrypted using a single seed block.

### Bit Constants

While very rare, there may be cases when the entire initial state is all zeroes. Diffusing bits that are all zeroes with each other does not generate a pseudorandom block but simply produces an all-zero block. Encrypting data with the all-zero block is dangerous as it does not encrypt the data at all since `m ⊕ 0 = m`.

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-xor-zero-block.txt") }}

To prevent the all-zero block, certain bits of the initial state block can always be set to one. In ChaCha20, the first four words (128 bits) of the initial state block are set to specific constants having non-zero values so that the four words, and by extension the entire block, will never be all zeroes.

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-words-constants.txt") }}

The constant values avoid the all-zero block, but more importantly these constants can also [introduce asymmetry](https://cr.yp.to/snuffle/security.pdf#page=5) if certain values are chosen. ChaCha20 has some rotational symmetry — different initial state blocks can generate the same output block, if the initial state blocks are specific [rotated](https://en.wikipedia.org/wiki/Group_action) versions of itself. Having fixed asymmetrical values for certain words eliminates the possibility of this shift/rotate structure.

The asymmetric constants form the first four words of the intial state block and have the values 0x61707865, 0x3320646e, 0x79622d32, 0x6b206574. There is [nothing special](https://en.wikipedia.org/wiki/Nothing-up-my-sleeve_number) about these constants — they simply spell "expand 32-byte k" in [ASCII](https://en.wikipedia.org/wiki/ASCII) in [little endian](https://en.wikipedia.org/wiki/Endianness#/media/File:32bit-Endianess.svg).

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-words-constants-values.txt") }}

### Shared Key

The constants, counter, and nonce values do not need to be exchanged securely — the counter and nonce keep changing often and it is impractical to securely exchange them frquently; while the constants too are public and standardised.

But even if half of the initial state block is non-secret, it is still secure since an attacker has to brute force the remaining 2^256 possible combinations for the remaining bits to guess the entire initial state block. This remaining half of the block, or eight words, is used for the actual 'key' and must be kept private between communicating parties.

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-block-words-all.txt") }}

The key along with the constants, counter and nonce generate the keystream.

{{ loadData(path="/static/media/lab/stream-ciphers/chacha-encryption.txt") }}

## Authenticated Encryption

Without the knowledge of the key, an attacker cannot easily guess the keystream and decrypt the ciphertext. But attackers can [modify the ciphertext](https://en.wikipedia.org/wiki/Bit-flipping_attack) itself — especially if they have some knowledge about the position of important bits in the plaintext stream.

{{ loadData(path="/static/media/lab/stream-ciphers/bit-flip-attack.txt") }}

{% tangent(summary="Calculating modified ciphertext", open=true) %}
If an attacker knows a certain string occurs at some position, they can modify it by replacing the ciphertext at that position by XOR-ing it with the original string and the modified string. So, if a part of original ciphertext is `c = m ⊕ k`, it can be replaced by `c' = (m ⊕ k) ⊕ m ⊕ m'`.

Decrypting `c'` results in `c' ⊕ k` = `(m ⊕ k ⊕ m ⊕ m') ⊕ k` = `m ⊕ m ⊕ k ⊕ k ⊕ m'` = `m'` — the modified message, without ever knowing the original key `k`.
{% end %}

ChaCha20 is not designed to detect nor protect against tampered ciphertexts. Because bit-flipping attacks can render the entire cipher useless, most stream ciphers are often paired with some sort of an authenticator to detect tampered ciphertexts. An encryption scheme that simultaneously encrypts a message as well as validates its authenticity is referred to as [authenticated encryption](https://en.wikipedia.org/wiki/Authenticated_encryption).

### Hashing

A simple (but rather naive) way to verify the integrity of a message is to simply compare the sum of all the bytes of the plaintext message and the decrypted ciphertext — a very primitive [checksum](https://en.wikipedia.org/wiki/Checksum). The checksum is usually calculated using modular addition to prevent the numbers from getting too big.

For example, the checksum of a message with bytes `C1`, `C2`, ... `Cq`, and an arbitrarily chosen integer `p` is:

`(C1 + C2 + ... + Cq-1 + Cq) mod p`

A sender can encrypt a message along with its checksum. The receiver can decrypt the message and compare the checksum of decrypted ciphertext with the one presented by the sender to verify its authenticity.

{{ loadData(path="/static/media/lab/stream-ciphers/hash-compare-checksum.txt") }}

However it is not secure at all. Attackers can modify a few bits of the ciphertext and still have a very high chance that the checksum of the decrypted modified ciphertext will still produce the same checkum as the original plaintext message. For it to be secure, the checksum must not output the same (colliding) values if its input message is different. In other words, the checksum must have adequate collision resistance.

{{ loadData(path="/static/media/lab/stream-ciphers/hash-compare-checksum-bit-flip.txt") }}

Instead of the naively adding all the bytes of the plaintext message, they can instead be evaluated as coefficients of a polynomial over a [prime field](https://en.wikipedia.org/wiki/Finite_field). That is, the checksum for a message having bytes `C1`, `C2`, ... `Cq` is:

`(C1·x^q + C2·x^(q-1) + ... + Cq-1·x^2 + Cq·x^1) mod p`

This is called a [polynomial rolling hash](https://en.wikipedia.org/wiki/Rolling_hash#Polynomial_rolling_hash), and the 'checksum' is called its hash. These hashes have much lower chances of collisions than the simple checksum method — for a well chosen integer `x` and big prime `p`.

{{ loadData(path="/static/media/lab/stream-ciphers/bit-flip-polynomial.txt") }}

{% tangent(summary="Hashing", open=true) %}
A [hash function](https://en.wikipedia.org/wiki/Hash_function) is any function that maps an input to a fixed sized output, called the hash. Both the simple checksum and the polynomial hash use modular addition and thus always map to fixed range outputs. So technically, both are hash functions.
{% end %}

{% tangent(summary="Prime field", open=true) %}
Performing the modulo operation limits the results to a finite set of elements. These elements form a [finite field](https://en.wikipedia.org/wiki/Finite_field) if the set satisfies certain [axioms](https://en.wikipedia.org/wiki/Field_(mathematics)#Definition) — properties of addition, subtraction, multiplication, and division must satisfied, for two defined binary operations. A prime field is a finite field with a prime number of elements.
{% end %}

Again, the hash presented by the sender is compared with hash of the decrypted ciphertext. If the hashes match, there should be a reasonable amount of confidence that the message is authentic and has not been altered — since the chances of collisions are much lower.

{{ loadData(path="/static/media/lab/stream-ciphers/hash-compare-bit-flip-polynomial.txt") }}

Since these hashes values are used to verify the authenticity of messages, they are aptly called [message authentication codes](https://en.wikipedia.org/wiki/Message_authentication_code) or authentication tags. MACs generated using hash functions are called hash-based MACs or [HMACs](https://en.wikipedia.org/wiki/HMAC).

{% tangent(summary="MAC criteria", open=true) %}
The above hash digests are technically not MACs because they are not considered to be adequately secure against forgeries. Generally, MACs use some shared secret information to verify the authenticity of messages.
{% end %}

### Keyed Hashing

The polynomial rolling hash acts on plaintext data, but ciphertexts can also be hashed. However, hashing the ciphertext (in this manner) is pointless. An adversary that can alter the ciphertext can also recalculate the hash of the altered ciphertext and then modify the MAC (hash) accordingly.

{{ loadData(path="/static/media/lab/stream-ciphers/hash-compare-recalculate-ciphertext.txt") }}

When the plaintext is hashed however, an attacker cannot easily calculate how a change in the ciphertext changes the resulting MAC — because the attacker does not have the knowledge about the complete plaintext to recalculate its hash.

{{ loadData(path="/static/media/lab/stream-ciphers/hash-compare-recalculate-plaintext.txt") }}

When the plaintext is hashed, an encrypted message must be decrypted before it can be verified — but it is not preferable because it is [not completely secure](https://moxie.org/2011/12/13/the-cryptographic-doom-principle.html). The alternative is generating the MAC from the ciphertext. However as mentioned earlier, MACs generated by hashing ciphertexts is even less secure.

The reason hashing ciphertexts to authenticate messages is not secure at all is because MACs are generated solely from a public ciphertext. However, if the MACs can include secret information only known to the communicating parties as its input, it can be much more secure. The secret information can again be a shared secret key.

{{ loadData(path="/static/media/lab/stream-ciphers/hash-compare-recalculate-ciphertext-with-secret.txt") }}

One way to embed the key in a MAC is to include the the key while the hashing it. Using the example of the polynomial rolling hash, the hash can be generated by evaluating the polynomial at the value of the key:

`MAC = (C1·k^q + C2·k^(q-1) + ... + Cq-1·k^2 + Cq·k^1) mod p`

Here `k` is the secret key, `p` is a sufficiently big prime and `C1`, `C2`, ... `Cq` are bytes of the **ciphertext**. Since the hash accepts a secret key alongside the message, this type of hashing is referred to as keyed hashing.

{{ loadData(path="/static/media/lab/stream-ciphers/hash-keyed-polynomial.txt") }}

But an even simpler way to include a secret key in a MAC is to simply add it to the hash of a ciphertext. Variable MACs or [VMACs](https://en.wikipedia.org/wiki/VMAC) function very similar to this — a hash function is used to hash a message, which is combined with a one-time key using addition:

`MAC = (H(c) + k) mod p`

For the VMAC to be secure, the hash function needs to be collision resistant, while the shared secret key `k` must be pseudorandom and must not be reused. Since the key is unique for every invocation, the MAC too is unique and varies every time, even for the same input — hence the name.

{{ loadData(path="/static/media/lab/stream-ciphers/hash-keyed-vmac.txt") }}

{% tangent(summary="VMAC as a masked hash", open=true) %}
The VMAC can be thought of as a hash being 'encrypted' or masked with the one-time pad `k`. For the VMAC to have (similar) security guarantees as the one-time pad, `k` must be (pseudo)random, and must never be reused.
{% end %}

Including a one-time key (technically a nonce) in the hash also makes it secure against [replay attacks](https://en.wikipedia.org/wiki/Replay_attack), since replayed messages (duplicate messages having the same nonces) can simply be trivially rejected by the receiver.

{{ loadData(path="/static/media/lab/stream-ciphers/replay-attack-rejection.txt") }}

MACs incorporating secret keys are much harder to forge, allowing them to be used for authenticating ciphertexts. An attacker can modify the ciphertext, but cannot recalculate its MAC without the knowledge of the secret key.

{{ loadData(path="/static/media/lab/stream-ciphers/hash-compare-keyed.txt") }}

## Poly1305

[Poly1305](https://en.wikipedia.org/wiki/Poly1305) is a hash function, that is often used for generating one-time MACs. When it is used for authentication, it behaves as a kind of VMAC using a keyed polynomial rolling hash as well as a one-time shared secret key. So the Poly1305 MAC for a ciphertext is:

`MAC = (H(C, r) + s) mod 2^128`\
`H(C, r) = (C1·r^q + C2·r^(q-1) + ... + Cq·r^1) mod p`

Where `H(C, r)` is a polynomial rolling hash using the bytes of the ciphertext `C` as its coefficients, evaluated at the point `r` over a prime field `p`. Meanwhile `s` is a secret one-time key. The MAC is the modular addition of the results of two operations, over a sufficiently big integer (2^128).

{{ loadData(path="/static/media/lab/stream-ciphers/poly1305-brief.txt") }}

In Poly1305 MAC, certain parameters have been unambigously defined:

The coefficients of the polynomial `C1`, `C2`, ... `Cq` are not single bytes of the input, but 16-byte chunks of the input interpreted as 17-byte chunks by appending a byte having the value one to each of the 16-byte chunks of the message. If the final chunk is smaller than 16-bytes, one is appended to the chunk and then zero padded to 17-bytes.

{{ loadData(path="/static/media/lab/stream-ciphers/poly1305-chunks.txt") }}

The inderminate of the polynomial, `r` is a shared secret key. It is a 16-byte little endian integer where the top four bits of bytes `r[3]`, `r[7]`, `r[11]`, and `r[15]`, as well as the bottom two bits of `r[4]`, `r[8]`, `r[12]` are all zeroes — to simplify and accelerate calculations.

{{ loadData(path="/static/media/lab/stream-ciphers/poly1305-key-r.txt") }}

The MAC is designed to be 128 bits long, and so the order of the prime field `p` should preferably be close to, and greater than 2^128. It was chosen to be 2^130 - 5 because its sparse form also [makes divisions easier](https://loup-vaillant.fr/tutorials/poly1305-design#poly1305s-prime-2130---5). The result is then reduced using modulo 2^128.

The other secret key `s` is a 128-bit pseudorandom number, which is added to the output of the polynomial rolling hash to mask it. The key `s` must never be reused.

{{ loadData(path="/static/media/lab/stream-ciphers/poly1305-key-s.txt") }}

The result is a 16 byte, or 128 bit MAC generated from an input `C` of arbitrary length, and two 16-byte secret keys `r` and `s`.

{{ loadData(path="/static/media/lab/stream-ciphers/poly1305-complete.txt") }}

## ChaCha20-Poly1305

Poly1305 can be used to authenticate ciphertexts generated using ChaCha20. The keys for Poly1305, `r` and `s` can be derived from the keys used for ChaCha20. However the 256-bit key used in ChaCha cannot directly be used in Poly1305 — because the key is persistent, but `s` should always be unique for every MAC.

{{ loadData(path="/static/media/lab/stream-ciphers/chachapoly-s-reuse.txt") }}

While the key used in ChaCha20 is persistent, its keystream is not — it is designed to generate unique keystreams for each message. Every time a new message needs to be authenticated, an extra pseudorandom block can be generated using ChaCha20, which can be used as the keys for Poly1305.

In ChaCha20-Poly1305, the extra block is generated by setting the counter of the initial state to zero for each new nonce (message). The rest of the keystream used to encrypt the plaintext message is generated by incrementing the counter, starting from one.

{{ loadData(path="/static/media/lab/stream-ciphers/chachapoly-s-from-keystream.txt") }}

The size of the pseudorandom block is 512 bits, but only 256 bits are required for the key pair `r` and `s`. So only the first 256 bits are used, while the remaining bits are discarded. The first 128 bits are used for `r` while the next 128-bits are used for `s`. Additionally, bits of `r` are clamped to satisfy its requirements — top four and bottom two bits of specific bytes must be zero.

{{ loadData(path="/static/media/lab/stream-ciphers/chachapoly-s-r.txt") }}

Because `r` and `s` are derived from a ChaCha20 block, which itself is dervied using a secret 256-bit key, the MAC cannot be easily forged without the knowledge of the 256-bit ChaCha20 key. The receiver of a message can then be reasonably confident that a message has not been been altered by anyone else and has been sent by someone having the same secret ChaCha20 key.

So messages are encrypted and authenticated using a single 256-bit key:

{{ loadData(path="/static/media/lab/stream-ciphers/chachapoly-encryption-authentication.txt") }}

It is worth noting that there are slight differences between ChaCha20 and the ChaCha20 used in ChaCha20-Poly1305. Unlike ChaCha20, the initial state in ChaCha20-Poly1305 uses a 32-bit counter and 96-bit nonce instead of a 64-bit counter and 64-bit nonce.

{{ loadData(path="/static/media/lab/stream-ciphers/chachapoly-block-words-seed.txt") }}

This allows more messages to be encrypted using the same key, albeit shorter ones. But it is not a problem, since a 32-bit counter still allows for encrypting messages of sizes up to 256 GiB.

### Associated Data

Sometimes ciphetexts can be paired with some associated plaintext data, which need not or should not be encrypted, but still need to be verified — data such as message timestamps, addresses, protocol versions, etc. This cleartext data is often sent alongside the ciphertext, and both are authenticated using a single MAC. This additional data is called associated data, and an authenticated encryption scheme that authenticates the associated data alongside the ciphertext, is aptly referred to as [authenticated encryption with associated data](https://en.wikipedia.org/wiki/Authenticated_encryption#Authenticated_encryption_with_associated_data), or AEAD.

ChaCha20-Poly1305 can authenticate ciphertext `C` along with some associated data `AD` by concatenating together, and treating them as a single unit to generate the MAC. The ChaCha20-Poly1305 specification defines `AD` and `C` to be separately padded to make their total sizes an even multiple of sixteen bytes. The padded `AD` and `C` as well as two other 64-bit fields, `len(AD)` and `len(C)`, are concatenated. Poly1305 then produces the MAC of the concatenated string.

{{ loadData(path="/static/media/lab/stream-ciphers/chachapoly-encryption-authentication-associated-data.txt") }}

{% tangent(summary="Message size limit", open=false) %}
While Poly1305 can be used for authenticating messages of arbitrary length, the 64-bit fields for `len(AD)` and `len(C)` restricts the possible size of the associated data `AD` and the ciphertext message `C` to 2^64 bits, or 16 EiB. But ciphertext `C` is further bottlenecked by the 32-bit counter of the ChaCha20 initial state — limiting message sizes to only 256 GiB. If required however, the ChaCha20-Poly1305 specification permits changing the counter to be set to its original size of 64 bits to allow encrypting and authenticating longer messages.
{% end %}

This is the entirety of [ChaCha20-Poly1305](https://en.wikipedia.org/wiki/ChaCha20-Poly1305), a stream cipher used to encrypt messages, and authenticate the encrypted messages along with some optional associated data. It used in [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security#TLS_1.3), [SSH](https://en.wikipedia.org/wiki/Secure_Shell#Algorithms), [WireGuard](https://en.wikipedia.org/wiki/WireGuard#Protocol), and [other protocols](https://en.wikipedia.org/wiki/ChaCha20-Poly1305#Use).

## Security Guarantees

The probability that attackers cannot decrypt a given ciphertext relies on the security of ChaCha20. Meanwhile the possibilities of forgeries depends on the security of Poly1305, as well as ChaCha20.

### Poly1305 Security

Since the output of Poly1305 is combined with a pseudorandom pad, it is as secure as the algorithm used to generate pseudorandom number. However, it does not imply that it is perfectly secure if the pad is purely random — since collisions are still possible, as the of the size of the MAC is [finite](https://en.wikipedia.org/wiki/Pigeonhole_principle).

Consider a prime field <i>GF(p)</i>, taken as <i>x mod p</i> where <i>x ∈ ℤ</i> and <i>p</i> is a prime. Then, for some polynomial of degree one, e.g. <i>a·x = h</i> where <i>a,x,h ∈ GF(p)</i> — there exists only one solution or root for <i>x</i>. The probability that <i>x</i> will produce <i>h</i> for a given <i>a</i> is <i>1/n</i>, where <i>n</i> is the number of all possible values for <i>x</i>. That is, <i>n = p</i>.

{{ loadData(path="/static/media/lab/stream-ciphers/security-poly1305-pf-one.txt") }}

For a polynomial of degree two, e.g. <i>a·x^2 + b·x = h</i>, there can be at most two solutions for <i>x</i>. The probability that <i>x</i> produces <i>h</i> for a given pair <i>a,b</i> is at most <i>2/n</i>. Where <i>n</i> is the total number of possible values for <i>x</i>. Here again, <i>n = p</i>.

{{ loadData(path="/static/media/lab/stream-ciphers/security-poly1305-pf-two.txt") }}

Similary, for a <i>q</i> degree polynomial, e.g. <i>C1·x^q + C2·x^(q-1) + ... + Cq·x^1 = h</i>, [there are at most](https://en.wikipedia.org/wiki/Fundamental_theorem_of_algebra) <i>q</i> number of roots for <i>x</i>, such that <i>x ∈ GF(p)</i>. Again, the probability that <i>x</i> produces <i>h</i> for some given coefficients is, at most <i>q/n</i> — where <i>n</i> is again the number of possible values for <i>x</i>.

Now assume a message <i>m</i> has a polynomial hash <i>h</i>. The probability of another distinct message <i>m'</i> having the same hash digest <i>h</i> will then depend on the on the degree of its polynomial. The polynomial in Poly1305 is of the form C1·r^q + C2·r^(q-1) + … + Cq·r^1. The coefficients of the polynomial are constructed from 16-byte chunks of a message, and thus, the degree of the polynomial is <i>⌈L/16⌉</i> — where <i>L</i> is the length of the message. So the probablity of a message <i>m'</i> having the (same) hash <i>h</i> is at most <i>⌈L/16⌉/n</i>.

{{ loadData(path="/static/media/lab/stream-ciphers/security-poly1305-pf-from-message.txt") }}

Since the indeterminate of the polynomial in Poly1305 <i>r</i> is a 128-bit number with 22 bits always set to zero, the number of possible values for <i>r</i> is 2^106. Thus, the probability of a message having a specific hash is at most <i>⌈L/16⌉/2^106</i>.

However, the polynomial is evaluated in <i>GF(p)</i> — the result is <i>h ∈ [0, 2^130 - 5)</i>, while the hash in Poly1305 is designed to be of 128 bits. So <i>h</i> is reduced modulo 2^128. Discarding two bits from <i>h</i> causes some outputs to be [congruent](https://en.wikipedia.org/wiki/Modular_arithmetic#Congruence) to others. More specifically, there are eight congurent values (mod 2^128) in <i>h</i> for every <i>H(m)</i> and <i>H(m')</i>.

{{ loadData(path="/static/media/lab/stream-ciphers/security-poly1305-congruency.txt") }}

This increases the differential probability to <i>8·⌈L/16⌉/2^106</i>, at most — because there are now eight times as many possibilities for two messages to have the same hash.

Now if <i>D</i> forgery attempts are made, then the probability of a single successful forgery is at most <i>D·8·⌈L/16⌉/2^106</i>. The probability of forgeries is [independent](https://cr.yp.to/mac/poly1305-20050329.pdf) of the number of messages authenticated — if the pad is [uniformly random](https://en.wikipedia.org/wiki/Discrete_uniform_distribution).

{% tangent(summary="Influence of the pad on probability of forgeries", open=false) %}
Generally, the pad is generated by a function <i>f</i> that maps a smaller nonce to a larger output space. If <i>f</i> has a uniform random distribution, then the probability that the pad is some specific number is <i>1/G</i>, where <i>G</i> is the total number of elements in the output space. If the probability the pad is a specific number is <i>1/G</i>, the probability that the pads are <i>C</i> specific numbers — or the probability that <i>f</i> interpolates <i>C</i> specific points is, at most <i>1/G · 1/G · ... · 1/G = 1/(G^C)</i>.

A uniform random [injective function](https://en.wikipedia.org/wiki/Injective_function) that has non-repeating nonces as its input can also be used for generating the pad. Then, the pad will not also repeat. The probability that it interpolates <i>C</i> number of distinct points is then <i>1/G · 1/(G-1) · 1/(G-2) · ... · 1/(G-(C-1))</i>. This can be simplified to <i>((1 − (C − 1)/G)^−(C/2))/(G)^C</i>. This can be used for evaluating the probability when [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) is used as <i>f</i> — e.g. in Poly1305-AES.

If <i>f</i> has a maximum C-interpolation probability at most <i>δ/(G^C)</i> and a maximum (C + 1)-interpolation probability at most <i>δε/(G^C)</i>, then the [probability of a successful forgery](https://cr.yp.to/antiforgery/securitywcs-20050227.pdf#page=9) using <i>C</i> distinct messages is <i>Dδε</i>, where <i>ε</i> is the probability of two messages having the same hash.

The pad in Poly1305 of ChaCha20-Poly1305 is generated using a ChaCha20 block, and can be assumed to have an interpolation probability of <i>1/(G^C)</i> as there is no restriction on pad repetition. So the probability of a successful forgery using <i>C</i> messages is at most <i>Dε</i>, or <i>D·8·⌈L/16⌉/2^106</i> — it is independent of the number of message authentications.

It is important to note that ChaCha20 blocks may still be distinguished from true random numbers with some different probability <i>δ</i>, which affects the overall probability of successful forgeries.
{% end %}

However, the Poly1305 pad in ChaCha20-Poly1305 is generated using a pseudorandom ChaCha20 block — it is not guaranteed to be truly uniformly random. If the probability of distinguishing a ChaCha20 block from a truly random keystream is <i>δ</i>, then the probability of a successful forgery is, at most <i>δ + D·8·⌈L/16⌉/2^106</i>.

### ChaCha20 Security

The randomness of the output of the ChaCha20 stream determines the security of the ciphertext, as well as the security of Poly1305. For true uniform randomness, each bit must have an equal probability of being zero or one.

Changing the initial state of a ChaCha20 block (even by a single bit flip) should ideally create a new uniform random block of bits. If the [initial state is changed](https://cr.yp.to/snuffle/security.pdf#page=5), the probability of any bit of the output block flipping [should be half](https://en.wikipedia.org/wiki/Avalanche_effect#Strict_avalanche_criterion) — on average, [half the bits should flip](https://en.wikipedia.org/wiki/Confusion_and_diffusion#Diffusion) for a change in the initial state. Or more specifically, the [number of bit flips](https://en.wikipedia.org/wiki/Hamming_distance) due to changes the inital state should form a [binomial distribution](https://en.wikipedia.org/wiki/Binomial_distribution) centered around half the bit length of the output block.

{{ loadData(path="/static/media/lab/stream-ciphers/security-chacha-diffusion.txt") }}

Empirical evidence suggests, it is the case. ChaCha20 produces output blocks that look uniformly random. Evaluating the randomess analytically is much more difficult however, because the interaction between the bits of the block quickly grows complex with each round. While there are ways to [measure the avalanche effect](https://webdoc.sub.gwdg.de/ebook/dissts/Bochum/Daum2005.pdf#page=57) — small changes flipping roughly half the bits, there is no proof that ChaCha20 blocks blocks can be distinguished (or not) from truly uniform random bitstreams.

There are however other ways to test its security — for example, using [linear](https://en.wikipedia.org/wiki/Linear_cryptanalysis), [differential](https://en.wikipedia.org/wiki/Differential_cryptanalysis) or [rotational](https://en.wikipedia.org/wiki/Rotational_cryptanalysis) [cryptanlysis](https://en.wikipedia.org/wiki/Cryptanalysis). ChaCha with six rounds has been [broken](https://cr.yp.to/streamciphers/attacks.html#chacha6), but there have been no successful attacks on twenty rounds of ChaCha.

ChaCha20-Poly1305, therefore is generally [considered secure](https://www.cryptrec.go.jp/exreport/cryptrec-ex-2601-2016.pdf).

---

## References

* Daniel J. Bernstein: [ChaCha, a variant of Salsa20](https://cr.yp.to/chacha/chacha-20080128.pdf)
* Daniel J. Bernstein: [The Poly1305-AES message-authentication code](https://cr.yp.to/mac/poly1305-20050329.pdf)
* IRTF RFC 8439: [ChaCha20 and Poly1305 for IETF Protocols](https://datatracker.ietf.org/doc/html/rfc8439)
