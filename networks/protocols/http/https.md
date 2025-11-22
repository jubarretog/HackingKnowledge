# HTTPS

**HTTPS** is the secure version of HTTP,  used to transfer data between web browsers and websites securely. All the data transmitted is encrypted using protocols like TLS (Transport Layer Security) or its predecessor, SSL (Secure Sockets Layer).

SSL (Secure Sockets Layer) is a protocol created to provide secure communication between two points using TCP as the basis. Its purpose was to guarantee a reliable and encrypted connection. However, all versions of SSL were compromised, especially SSL v3.

Its replacement was TLS (Transport Layer Security), which is based on SSLv3, but was enhanced to provide secure communication with greater guarantees, offering confidentiality via encryption, integrity by detecting tampering, and non-repudiation by verifying authenticity.

## <mark style="color:blue;">TLS Handshake Flow</mark>

TLS uses an authentication and algorithm negotiation flow that combines symmetric, asymmetric, and integrity encryption algorithms. Following, we find the flow steps of the TLS communication:

* **ClientHello:** The client initiates the connection by sending a ClientHello message with:
  * The highest version of the TLS protocol it supports
  * A list of supported encryption algorithms
  * Client random bytes
  * Other optional data, like session identifier, extensions, and supported methods
* **ServerHello:** The server responds by selecting the connection parameters from those offered by the client and sending the values in a ServerHello message with:
  * Chosen TLS version
  * Chosen cipher suite. For example, _TLS\_DHE\_RSA\_WITH\_AES\_256\_CBC\_SHA_ indicates that it will use:
    * TLS as a transport protocol
    * DHE (Diffie-Hellman Ephemeral) for the key agreement
    * RSA for authentication
    * AES 256-bit AES for symmetric encryption
    * SHA-256 for integrity
  * Session ID
  * Server random bytes
  * Other optional data
* **Server Certificate:** The server sends its digital certificate, which allows the client to authenticate the server’s identity
* **ServerKeyExchange/CertificateRequest:** If the selected key exchange uses ephemeral keys, the server may send a ServerKeyExchange message, and if client authentication is required, the server sends CertificateRequest
* **ServerHelloDone:** The server signals the end of its hello phase **with a ServerHelloDone message**
* **Client Certificate (Optional):** If client authentication is requested, the client sends its certificate
* **ClientKeyExchange:** Client and server negotiate a symmetric secret key called _master secret_, using the result of a Diffie-Hellman exchange, or simply encrypting a secret key with a public key that is decrypted with each other's private key
* **CertificateVerify (Optional):** If the client sent the optional certificate, it must prove possession of the private key via the **CertificateVerify** message
* **ChangeCipherSpec:** Both client and server send a ChangeCipherSpec message to notify that subsequent messages will be encrypted
* **Finished:** Both parties sent a Finished message to start communicating via HTTPS
