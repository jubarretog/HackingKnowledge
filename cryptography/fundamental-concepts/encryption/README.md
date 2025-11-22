# Encryption

**Encryption** is the process of converting data into an unreadable format to ensure confidentiality. Its crucial center is that it relies on cryptographic algorithms and one or more keys to protect information from unauthorized access.

Unlike encoding, encryption is designed to be reversible only for those who have the correct key, making it essential for secure communication, data protection, and privacy.

A main concept in cryptography is the Key Size, which refers to the number of bits used in a cryptographic key. This gives a measure of how many possible different keys there are, and the resistance against brute-force attacks. For example, a 128-bit key has 2<sup>128</sup> possible combinations, a 256-bit key has 2<sup>256</sup> possible combinations, and so on.

It is also important to implement encryption correctly and to use strong keys to avoid possible attacks and maintain the data secure. There are two main types of encryption, which are used in different scenarios, with necessities like security, speed, efficiency, and ease of use that need to be covered.&#x20;

## <mark style="color:blue;">**Symmetric**</mark>

Also called secret-key encryption, uses the same key for both encryption and decryption. It’s fast, efficient, and ideal for encrypting large volumes of data.

<figure><img src="../../../.gitbook/assets/image (938).png" alt="" width="563"><figcaption><p><a href="https://miro.medium.com/v2/resize:fit:1400/1*62blCQs9eJ9MPxY7q27aCg.jpeg">https://miro.medium.com/v2/resize:fit:1400/1*62blCQs9eJ9MPxY7q27aCg.jpeg</a></p></figcaption></figure>

It's important to know that if the key is compromised, all of the data that was encrypted with that key will be able to be decrypted.

Its main characteristics are:

* Both parties need to share the secret key before the communication and keep it secure
* Used when the priority is speed and efficiency are priority
* Faster than symmetric encryption but with less key size
* Usually used to protect files, communications, databases, embedded systems, and secure tunnels in network protocols such as VPNs, TLS, or SSH
* Some examples are AES,  &#x20;DES,  &#x20;3DES,  &#x20;RC4, Blowfish

## <mark style="color:blue;">Asymmetric</mark>

Asymmetric encryption uses a pair of keys, the first one known as the public key, to encrypt the information, and the second one as the private key, to decrypt it. The public key can be shared with anyone, but the private key must be kept secret.

<figure><img src="../../../.gitbook/assets/image (939).png" alt="" width="563"><figcaption><p><a href="https://miro.medium.com/v2/resize:fit:1100/format:webp/1*duPa4Dykr9-18cpCeHTiWg.jpeg">https://miro.medium.com/v2/resize:fit:1100/format:webp/1*duPa4Dykr9-18cpCeHTiWg.jpeg</a></p></figcaption></figure>

The sender uses the public key of the recipient to encrypt the data, and in this way, the data can only be decrypted with the private key of the same recipient.

It's widely used in secure messaging, digital signatures, and key exchange.

* Slower than symmetric encryption, but considered more secure, as the secret is only known by the owner and not shared with anyone
* Typically used for encrypting small amounts of data, secure key exchange, and digital signatures
* Some examples are RSA, DSA, ECDH, ECC

### <mark style="color:purple;">Signatures</mark>

Signatures are used to provide authentication, integrity, and non-repudiation of data. Unlike encryption, which hides content, a signature confirms that a message or file was genuinely created by a known sender and has not been altered in transit.

It works oppositely to the encryption process, where a user uses the private key to sign a message, and anyone can use the corresponding public key to verify it. This creates a verifiable link between the message and the signer without revealing the private key.

<figure><img src="../../../.gitbook/assets/image (925).png" alt="" width="463"><figcaption><p><a href="https://comodosslstore.com/blog/what-is-digital-signature-how-does-it-work.html">https://comodosslstore.com/blog/what-is-digital-signature-how-does-it-work.html</a></p></figcaption></figure>

A stablished practice in signatures is first hashing the original data before signing it, instead of signing the full message directly. This makes signing efficient and ensures that even the slightest change in the original message leads to a completely different signature, ensuring data integrity and source authenticity.

Digital signatures are widely used in:

* Secure software updates and package signing
* TLS certificates for HTTPS
* Email authenticity (PGP, S/MIME)
* Blockchain transactions

It is vital to use secure key lengths, resistant hash functions, and proper padding schemes to avoid signature forgery and hash collision attacks, as well as secure implementation and key management.

### <mark style="color:purple;">Public and Private Key Role Importance</mark>

The public and private keys have specific roles to allow operations to be reversed and verified correctly.  These have to be respected to maintain the purposes of operations without compromising confidentiality or authenticity.

For example, let's think of a reversed scenario for encryption:

* The public is only known by the owner, and the private key is known by everyone
* This means that anyone could decrypt messages meant for us, as everyone has our private key, and nobody could encrypt a message for us, as anyone has our public key
* The result is that there is no confidentiality, as no one can send us encrypted messages, and any encrypted data is public

Now, let's think of a reversed scenario for encryption:

* Only the owner has the public key, and everyone has the private key
* This means that anyone could generate a signature pretending to be us, and only we could verify it, but no one else could trust it
* The result is that the signatures are meaningless, as anyone can forge them, and no one else can verify them

In conclusion, the public and private keys cannot be arbitrarily swapped unless the context explicitly allows it:

* Encrypting a message with a private key is not encryption in the confidentiality sense; it’s signing
* Decrypting with a public key is not decryption in the confidentiality sense; it’s signature verification
* For secrecy, we must use the flow _public → private,_ and for authenticity, the flow _private → public_
