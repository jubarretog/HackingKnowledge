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



* Generate private key with RSA

{% code overflow="wrap" lineNumbers="true" %}
```bash
openssl genrsa -out $name 2048
```
{% endcode %}
