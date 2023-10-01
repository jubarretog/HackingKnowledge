# Tools

## <mark style="color:green;">Openssl</mark>

### **Characteristics**

* Tool-kit for cryptography
* Generate keys and certificates
* Encrypt and Dcrypt data and tipical ciphers

### **Commands**

* Conecct as a client

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



## <mark style="color:green;">John the ripper</mark>

* Broke hash

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo john -w=$wordlist $hashfile
```
{% endcode %}

***



## <mark style="color:green;">Dcode.fr</mark>

### **Characteristics**

* Online tool for encrypting, decrypting, coding or decoding cyphers
* Can identified what cipher is used in a ciphertext
* [https://www.dcode.fr/cipher-identifier](https://www.dcode.fr/cipher-identifier)

***



## <mark style="color:green;">Cyberchef</mark>

### **Characteristics**

* Online tool for encrypting, decrypting, coding or decoding cyphers
* With the magic mode try to identify and decode automatically the ciphertext
* [https://gchq.github.io/CyberChef/](https://gchq.github.io/CyberChef/)

***



gzip, tar, unzip, 7z, gpg
