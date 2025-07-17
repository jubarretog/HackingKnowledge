# Encryption (WIP)

**Encryption** is the process of converting data into an unreadable format to ensure confidentiality. Its crucial center is that it relies on cryptographic algorithms and one or more keys to protect information from unauthorized access.

Unlike encoding, encryption is designed to be reversible only for those who have the correct key, making it essential for secure communication, data protection, and privacy.

A main concept in cryptography is the Key Size, which refers to the number of bits used in a cryptographic key. This gives a measure of how many possible different keys there are, and the resistance against brute-force attacks. For example, a 128-bit key has 2<sup>128</sup> possible combinations, a 256-bit key has 2<sup>256</sup> possible combinations, and so on.

There are two main types of encryption, which have different characteristics and cases of use:

## <mark style="color:blue;">**Symmetric**</mark>

Also called secret-key encryption, uses the same key for both encryption and decryption. It’s fast, efficient, and ideal for encrypting large volumes of data.

<figure><img src="../../../.gitbook/assets/image (914).png" alt="" width="563"><figcaption><p><a href="https://miro.medium.com/v2/resize:fit:1400/1*62blCQs9eJ9MPxY7q27aCg.jpeg">https://miro.medium.com/v2/resize:fit:1400/1*62blCQs9eJ9MPxY7q27aCg.jpeg</a></p></figcaption></figure>

Its main characteristics are:

* Used when the priority is speed and efficiency are priority
* Usually used to protect files, communications, databases, embedded systems, and secure tunnels in network protocols such as VPNs, TLS, or SSH
* Faster than symmetric encryption but with less key size
* Both parties need to share the secret key before the communication and keep it secure
* Some examples are AES,  &#x20;DES,  &#x20;3DES,  &#x20;RC4, Blowfish

## <mark style="color:blue;">Asymmetric</mark>

Asymmetric encryption uses a pair of keys, the first one known as the public key, to encrypt the information, and the second one as the private key, to decrypt it. The public key can be shared with anyone, but the private key must be kept secret.

<figure><img src="../../../.gitbook/assets/image (915).png" alt="" width="563"><figcaption><p><a href="https://miro.medium.com/v2/resize:fit:1100/format:webp/1*duPa4Dykr9-18cpCeHTiWg.jpeg">https://miro.medium.com/v2/resize:fit:1100/format:webp/1*duPa4Dykr9-18cpCeHTiWg.jpeg</a></p></figcaption></figure>

It's widely used in secure messaging, digital signatures, and key exchange.

* Typically used for secure key exchange and digital signatures
* Slower than symmetric encryption, but it is more secure as the private key is never shared with anyone
* Some examples are RSA, DSA, ECDH, ECC



Your reversed scenario:

Only you know the public key

Everyone knows the private key

🧨 What happens?

Anyone can decrypt messages meant for you (they have the private key)

Nobody can encrypt a message for you (they don’t have your public key)

🟥 Result: No confidentiality. No one can send you secret messages, and any encrypted data is public.



### <mark style="color:purple;">Signatures</mark>

Private to encrypt, public to decrypt. authentication



**Your reversed scenario:**

* Everyone has the **private key**
* Only you have the **public key**

🧨 **What happens?**

* **Anyone** can generate a signature pretending to be you
* **Only you** can verify it (but no one else can trust it)

🟥 **Result**: Signatures are meaningless — anyone can forge them, and no one else can verify them.
