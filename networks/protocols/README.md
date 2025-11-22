# Protocols

**Network protocols** are the set of rules and conventions that govern how data is transmitted, received, and interpreted across a network, including its structure and components. These protocols ensure that devices, systems, and applications can communicate efficiently and securely, regardless of their underlying infrastructure.&#x20;

<figure><img src="../../.gitbook/assets/image (27) (1) (1).png" alt="" width="344"><figcaption></figcaption></figure>

They play a crucial role in maintaining the integrity and reliability of communications over the Internet, local networks, and private systems, by defining standards from data formatting to error checking and packet routing.&#x20;

Here is a list of some well-known network protocols:

* **ARP:** Address Resolution Protocol, operates in the Data Link layer, and is responsible for finding the MAC address related to a specific IP address
* **PPP:** Point-to-Point Protocol operates in the Data Link layer, used to establish a direct connection between two nodes of a network
* **DHCP:** Dynamic Host Configuration Protocol operates in the Data Link layer, and is used to automatically assign IP addresses and other network configuration parameters to devices on a network. Usually operates on UDP ports 67/68 and communicates by sending the following messages:
  * **DHCP Discover:** See if any DHCP servers are on the network
  * **DHCP Offer:** The DHCP server then replies with an IP address that could be used
  * **DHCP Request:** The device replies confirming it wants the offered IP Address
  * **DHCP ACK:** The DHCP server sends a reply acknowledging that this has been completed, and the device can start using the IP Address
* **ICMP:** Internet Control Message Protocol operates in the Network layer and diagnoses route state through error messages
* **TCP:** Transmission Control Protocol is a connection-based protocol that operates in the Transport layer, and is used when accuracy is more important than speed, dividing the transmission into _segments_
* **UDP:** User Datagram Protocol, a protocol that operates in the Transport layer, is used when speed is more important than accuracy, dividing the transmission into _datagrams_
* **FTP:** File Transfer Protocol, operates in the Application layer, sending and receiving files between systems connected through TCP. Usually operates on port 21
* **TFTP:** Trivial File Transfer Protocol, operates in the Application layer, using it is only possible to upload and download files from a server. Usually operates on UDP port 69
* **DNS:** Domain Name System, operates in the Application layer, transforms domain URLs into IP addresses and vice versa. Usually operates on UDP port 53
* **HTTP:** HyperText Transfer Protocol operates in the Application layer, a set of rules used for communicating with web servers for the transmission of data. Usually operates on port 80
* **HTTPS:** HyperText Transfer Protocol Secure, operates in the Application layer, is the secure version of _HTTP,_ where data is encrypted, and stops people from seeing the sent or received data. Usually operates on port 443
* **WHOIS:**  Operates in the Application layer, queries databases that store information about domain names, IP addresses, and related entities. Usually operates on port 43
* **SSH:** Secure Shell Protocol operates in the Application layer and manages remote access to a server via a secure channel. Allows remote execution of commands on another device. Any data between devices is encrypted when traveling through the network. Usually operates on port 22
* **Telnet:**  Operates in the Application layer, and is used for terminal-to-terminal connections, and by other protocols to establish a remote control channel. Usually operates on port 23
* **SMB:** Server Message Block, operates in the Application layer, a client-server protocol that controls file and directory access and other network resources. It is used a lot in _Windows_ for file transfer or sending files to printers. Usually operates on port 445
* **NTP:** Network Time Protocol, operates in the Application layer, an internet protocol that synchronizes system clocks via packet routing with a variable latency. Usually operates on UDP port 123
* **IRC:** Internet Relay Chat operates in the Application layer, and is based on real-time communication for chat channels where no previous communication has to be established between users. Usually operates on port 194
* **RIP:** Routing Information Protocol operates in the Application layer, and is used by routers for exchanging information about IP networks. Usually operates on UDP port 520
* **SNMP:** Simple Network Management Protocol operates in the Application layer, facilitates the exchange of management information between network devices, and allows administrators to monitor the operation of the network. Usually operates on UDP ports 161/162
* **SMTP:** Simple Mail Transfer Protocol, operates in the Application layer, used for sending and receiving e-mail. Usually operates on port 25
* **SMTPS:** Simple Mail Transfer Protocol Secure, operates in the Application layer, a variant of _SMTP_ that uses _SSL/TLS_ encryption to securely send emails. Usually operates on port 465
* **POP:** Post Office Protocol, usually POP3, operates in the Application layer, and is used by local clients to get and manage mail messages from a remote POP server. Usually operates on port 110
* **UPnP:** Universal Plug and Play operates in the Application layer, allowing devices to discover each other in a network and establish network services. Usually operates on UDP port 1900
