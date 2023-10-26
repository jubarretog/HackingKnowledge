# Tools

## <mark style="color:green;">Openssl</mark>

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
sudo john -w=$wordlist $hashfile
```
{% endcode %}

***



## <mark style="color:green;">Hashcat</mark>

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

***



## <mark style="color:green;">Dcode.fr</mark>

* Online tool for encrypting, decrypting, coding or decoding cyphers
* Can identified what cipher is used in a ciphertext
* [https://www.dcode.fr/cipher-identifier](https://www.dcode.fr/cipher-identifier)



## <mark style="color:green;">Cyberchef</mark>

* Online tool for encrypting, decrypting, coding or decoding cyphers
* With the magic mode try to identify and decode automatically the ciphertext
* [https://gchq.github.io/CyberChef/](https://gchq.github.io/CyberChef/)
