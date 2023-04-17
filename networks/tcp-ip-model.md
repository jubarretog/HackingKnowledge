# TCP/IP Model

Implements TCP to control the flow of data between two endpoints, and the IP to control how packets are addressed are sent. With TCP/IP any data that is lost or corrupted on transmission is re-sent

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* TCP/IP uses a method called _Three-way handshake_ to stablish connection between devices. It works as following:
  * A request is sent with a _"synchronise"_ bit named _SYN_ to make first contact with server.
  * If _SYN_ is send to a closed port, the target server will respond with a TCP packet called _RST_ Reset) is return to client and connection is reected
  * If reach an open port, the server will then respond with a packet containing the _SYN_ bit, as well as another _"acknowledgement"_ bit, called _ACK_.
  * Initial device will send a packet that contains the _ACK_ bit by itself, confirming that the connection has been setup successfully.
  * Then connection can be stablished using TCP
