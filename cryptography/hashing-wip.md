---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Hashing

Hashing is a process used to convert data of any size into a fixed-length string of characters, usually through a mathematical algorithm. Unlike encryption, which can be reversed (decrypted), hashing is a one-way function, meaning that the original data cannot be recovered from the hash.&#x20;

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="375"><figcaption></figcaption></figure>

For example, when a file or password is hashed, any slight change in the input data will produce a completely different hash value. This makes it ideal for detecting changes in data and ensuring that files or messages haven't been altered.

## <mark style="color:blue;">Well-known hashes</mark>

* LM hash or NTLM hash
* SHA256crypt and SHA512crypt: Linux incorporated hashing for passwords
* MD5 Hash
* SHA-1

