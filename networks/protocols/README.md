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

# Protocols

Network protocols are the set of rules and conventions that govern how data is transmitted, received, and interpreted across a network. These protocols ensure that devices, systems, and applications can communicate efficiently and securely, regardless of their underlying infrastructure.&#x20;

<figure><img src="../../.gitbook/assets/image (27).png" alt="" width="344"><figcaption></figcaption></figure>

They play a crucial role in maintaining the integrity and reliability of communications over the Internet, local networks, and private systems, by defining standards from data formatting to error checking and packet routing.&#x20;

Here we find a list of the most well-known network protocols:

* **ICMP:** Internet Control Message Protocol, occurs in the network layer, and diagnoses route state through error messages.
* **ARP:** Address Resolution Protocol, responsible for finding the MAC address related to a specific IP address.
  * A request is sent to every other device in the network. This is known as _Broadcast_.
  * The device whose IP matches replies to the initial device with the MAC address.
* **DHCP:** Dynamic Host Configuration Protocol, communicate via sending the following messages:
  * **DHCP Discover:** See if any DHCP servers are on the network.
  * **DHCP Offer:** The DHCP server then replies with an IP address that could be used.
  * **DHCP Request:** The device replies confirming it wants the offered IP Address.
  * **DHCP ACK:** The DHCP server sends a reply acknowledging this has been completed, and the device can start using the IP Address.
* **TCP:** Transmission Control Protocol, is a connection-based protocol that occurs in the transport layer, and would be used when accuracy is more important than speed. Divide the transmission into _segments_.
* **UDP:** User Datagram Protocol, which occurs in the transport layer, would be used when speed is more important than accuracy. Divide the transmission in _datagrams_.
* **FTP:** File Transfer Protocol, which occurs in the application layer, sends and receives files between systems connected through TCP.
* **TFTP:** Trivial File Transfer Protocol.
* **DNS:** Domain Name System, is a TCP/IP protocol that transforms domain URLs into IP addresses.
* **HTTP:** HyperText Transfer Protocol, a set of rules used for communicating with web servers for the transmitting of webpage data. The usual port to access is 80.
* **HTTPS:** HyperText Transfer Protocol Secure, is the secure version of HTTP where data is encrypted, and stops people from seeing the data you are receiving and sending. The usual port to access is 443.
* **WHOIS:** Listens on TCP port 43 for incoming requests, server replies with various information related to the domain requested.
* **SSH:** Secure Shell, Protocol, and program that lets remote access to a server via a secure channel. Allows us to remotely execute commands on another device. Any data between devices is encrypted went travels through the network. It listens on port 22.
* **Telnet:** Used for terminal-to-terminal connections and used by other protocols to establish a Remote Control Channel. Usually used in port 23.
* **SMB:** Server Message Block, a client-server protocol that controls file and directory access and other network resources, it is used a lot in Windows for file transfer or sending files to printers. The default port is 445.
* **IRC:** Interner Realy Chat.
* **NTP:** Network Time Protocol, an internet protocol that synchronizes system clocks via packet routing in a variable latency. Occurs on the transport layer using port 123.
* **IRC:** Internet Relay Chat, a protocol based on real-time communication for chat channels where no previous communication has to be established between users. Use port 194.
* **RIP:** Routing Information Protocol, used by routers for exchanging information about IP networks. Uses port 520.
* **SNMP:** Simple Network Management Protocol, facilitates the exchange of management information between network devices and allows administrators to monitor the operation of the network. Uses port 161/162 UDP
* **SMTP:** Simple Mail Transfer Protocol, occurs in the application layer used for sending and reception of e-mail. Uses port 25.
* **SMTPS:** Simple Mail Transfer Protocol Secure, uses port 587.
* **PPP:** Point-to-Point Protocol, occurs on the data link layer, used to establish a direct connection between to nodes of a network.
* **POP:** Post Office Protocol, normally POP3, is used by local clients to get and manage mail messages from a remote POP server.
* **SNMP:** Simple Network Management Protocol**,** is a network layer protocol based on IP which interchange information between enabled devices and the network management solution.
