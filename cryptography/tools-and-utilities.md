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

# Tools and Utilities

Here we can find some tools and utilities commonly used for processes related to cryptography:

## <mark style="color:green;">OpenSSL</mark>

* Tool-kit for cryptography
* Generate keys and certificates
* Encrypt and Decrypt data and typical ciphers

### <mark style="color:yellow;">**Commands**</mark>

* Connect as a client

{% code overflow="wrap" lineNumbers="true" %}
```bash
openssl s_client -connect $IP:$port
```
{% endcode %}

***

* Generate private key with RSA

{% code overflow="wrap" lineNumbers="true" %}
```bash
openssl genrsa -out $name 2048
```
{% endcode %}

***

* Generate hash for Linux user

{% code overflow="wrap" lineNumbers="true" %}
```bash
openssl passwd -1 -salt AAA $password
```
{% endcode %}

## <mark style="color:green;">John the ripper</mark>

* Password cracking tool, known for its speed and efficiency in cracking weak passwords.

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install john
```
{% endcode %}

***

* Broke hash

{% code overflow="wrap" lineNumbers="true" %}
```bash
john -w=$wordlist $hashfile
```
{% endcode %}

{% hint style="info" %}
One famous dictionary is _rockyou.txt_ which can be found by default on Kali Linux on _/usr/share/wordlists/rockyou.txt_
{% endhint %}

***

* Use unshadow to create a crackable file

{% code overflow="wrap" lineNumbers="true" %}
```bash
unshadow $passwdFile $shadowFile > $outFile
#passwdFile and shadowFile are the /etc/passwd and /etc/shadow files respectively
```
{% endcode %}

## <mark style="color:green;">Hashcat</mark>

* Password recovery tool that supports a wide range of hashing algorithms, primarily used for cracking passwords stored in hashed formats.

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install hashcat
```
{% endcode %}

***

* Filter code of a hash mode

{% code overflow="wrap" lineNumbers="true" %}
```bash
hashcat --help | grep -i $keyword
```
{% endcode %}

***

* Attack hash

{% code overflow="wrap" lineNumbers="true" %}
```bash
hashcat -a $attackmode -m $modecode $file.hash $dictionary
```
{% endcode %}

## <mark style="color:green;">Dcode.fr</mark>

* Online tool for encrypting, decrypting, encoding, or decoding ciphers
* [https://www.dcode.fr/en](https://www.dcode.fr/en)

{% hint style="info" %}
Have a cipher identifier: [https://www.dcode.fr/cipher-identifier](https://www.dcode.fr/cipher-identifier)
{% endhint %}

## <mark style="color:green;">Cyberchef</mark>

* Online tool for encrypting, decrypting, encoding, or decoding ciphers
* [https://gchq.github.io/CyberChef/](https://gchq.github.io/CyberChef/)

{% hint style="info" %}
The magic mode helps you identify and decode automatically the ciphertext
{% endhint %}