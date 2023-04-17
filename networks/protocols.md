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
* **DNS:** Domain Name System, is an TCP/IP protocol which transforms domain URL into IP adresses.
* **HTTP:** HyperText Tranfer Protocol, set of rules used for communicating with web servers for the transmitting of webpage data. Usual port is to access is 80.
* **HTTPS:** HyperText Transfer Protocol Secure, is the secure version of HTTP where data is encrypted, stops people from seeing the data you are receiving and sending. Usual port is to access is 443.
* WHOIS: Listens on TCP port 43 for incoming requests, server replies with various information related to the domain requested.
