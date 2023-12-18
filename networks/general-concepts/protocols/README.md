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

* **ICMP:** Internet Control Message Protocol, occurs in network layer, diagnose route state through error messages.
* **ARP:** Address Resolution Protocol, responsible for finding the MAC address related to a specific IP address.
  * A request is sent broadcasted to every other device in the network.
  * The device whose IP matches replies to the initial device with the MAC adress.
* **DHCP:** Dynamic Host Configuration Protocol,communicate via sengind the following messages:
  * _DHCP Discover:_ See if any DHCP servers are on the network.
  * _DHCP Offer:_ DHCP server then replies back with an IP address that could use.
  * _DHCP Request:_ Device replies confirming it wants the offered IP Address.
  * _DHCP ACK:_ DHCP server sends a reply acknowledging this has been completed, and the device can start using the IP Address.
* **TCP:** Transmission Control Protocol, is a connection-based protocol that occurs in transport layer, would be used when accuracy is more important than speed. Divide the transmission in _segments_.
* **UDP:** User Datagram Protocol, occurs in transport layer, would be used when speed is more important than accuracy. Divide the transmission in _datagrams_.
* **FTP:** File Transfer Protocol, occurs in application layer, send and recieved files bweteen systems connected through TCP.
* **TFTP:** Trivial File Transfer Protocol.
* **DNS:** Domain Name System, is an TCP/IP protocol which transforms domain URL into IP adresses.
* **HTTP:** HyperText Tranfer Protocol, set of rules used for communicating with web servers for the transmitting of webpage data. Usual port is to access is 80.
* **HTTPS:** HyperText Transfer Protocol Secure, is the secure version of HTTP where data is encrypted, stops people from seeing the data you are receiving and sending. Usual port to access is 443.
* **WHOIS:** Listens on TCP port 43 for incoming requests, server replies with various information related to the domain requested.
* **SSH:** Secure Shell, Protocol and program wich let remote access to a server via a secure channel. Allows us to remotely execute commands on another device.Any data between devices is encrypted went traveling through network. It listens on port 22.
* **Telnet:** Used for terminal to terminal conections and used by other protocols to stablish a Remote Control Chanel. Usually used in port 23.
* **SMB:** Server Message Block, client-server protocol that control file and directory access and other network resources, it is used a lot in Windows for file transfer or sending files to printers. Default port is 445.
* **IRC:** Interner Realy Chat.
* **NTP:** Network Time Protocol, internet protocol that synchronize system clocks via packets routing in a variable latency. Occurs on transport layer using port 123.
* **IRC:** Internet Relay Chat, comunication protocol real time based for chat channelss where no previous comunication has to be stablished between users. Use port 194.
* **RIP:** Routing Information Protocol, used by routers for exchanging information about IP networks. Uses por 520.
* **SNMP:** Simple Network Management Protocol, facilitates the exchange of management information between network devices and allows administrators to monitor the operation of the network. Uses port 161/162 UDP
* **SMTP:** Simple Mail transfer Protocol, occurs in aplication layer used for sending and reception of e-mail. Uses port 25.
* **SMTPS:** Simple Mail transfer Protocol Secure, uses port 587.
* **PPP:** Point-to-Point Protocol, occurs on data link layer, used to stablish a direct connection between to nodes of a network.
* **POP:** Post Office Protocol, normally POP3, used in local clients to get and manage mail messages from a remote POP server.

