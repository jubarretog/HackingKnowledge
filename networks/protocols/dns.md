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

# TCP

The **Transmission Control Protocol** provides reliable, connection-oriented communication using features like error checking, flow control, and validation. Is used in applications requiring data integrity, like web browsing, emails, and file transfers.

It uses a method called _Three-way Handshake_ to establish a connection between devices. It works as follows:

* A request is sent with a bit named _SYN_ (Synchronize) to make the first contact with the server
* If _SYN_ is sent to a closed port, the target server will respond with a TCP packet called _RST (_&#x52;eset) which is returned to the client, and the connection will be rejected
* If reaches an open port, the server will then respond with a packet containing the _SYN_ bit, as well as another bit, called _ACK_ (Acknowledgment)
* The initial device will send a packet that contains the _ACK_ bit by itself, confirming that the connection has been set up successfully
* Then, the connection can be established using TCP
