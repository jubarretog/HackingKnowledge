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

# TCP/IP Model

Implements the TCP protocol to control the flow of data between two endpoints, and the Internet Protocol (IP) to control how packets are addressed and sent. With TCP/IP any data that is lost or corrupted on transmission is re-sent.

<figure><img src="../../.gitbook/assets/image (280).png" alt=""><figcaption></figcaption></figure>

The TCP/IP model uses a method called _Three-way Handshake_ to establish a connection between devices. It works as follows:

* A request is sent with a bit named _SYN_ (Synchronize) to make the first contact with the server.
* If _SYN_ is sent to a closed port, the target server will respond with a TCP packet called _RST (_Reset) which is returned to the client, and the connection will be rejected.
* If reaches an open port, the server will then respond with a packet containing the _SYN_ bit, as well as another bit, called _ACK_ (Acknowledgment).
* The initial device will send a packet that contains the _ACK_ bit by itself, confirming that the connection has been set up successfully.
* Then, the connection can be established using TCP.
