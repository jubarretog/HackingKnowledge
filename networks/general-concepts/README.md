# General Concepts

* **NIC:** Network Interface Card
* **Routing:** Process of data traveling through a network
* **ISP:** Internet Service Provider.
* **Public address:** Used to identify the device on the Internet, are given by teh ISP.
* **Private address:** Used to identify a device amongst other devices.
* **MAC adress:** Media Access Control, is a hardware address set by the manufacturer in network interface cards. It's a twelve-character hexadecimal number. The first six characters represent the company that made the network interface, and the last six is a unique number.
* **IP adress:** Internet Protocol address, identify a host on a network and can't be active simultaneously more than once within the same network. It's conformed by 4 octets of bits, each octate representes a number in range 0-255.
* **LAN:** Local Area Network.
* **Ping:** Way to send ICMP packets to determine the performance of a connection between devices.
* **SCP:** Secure File Copy, transfer files between two computers using the SSH protocol to provide authentication and encryption.
* **Switch:** Device designed to aggregate multiple other networking-capable device using ethernet.Sends the package only to the intended target, thus reducing network traffic.
* **Repeaters:** Same function as switch but replays sent information to all devices connected to it.
* **Router:** Connects networks and pass data between them.
* **Network Address** Identifies the start of the actual network.
* **Host Address:** Used to identify a device on the subnet.
* **Default Gateway:** Special address assigned to a device on the network that is capable of sending information to another network.
* **Encapsulation:** The process of data getting added information details as it goes through every layer before getting send.
* **De-Encapsulation:** Reverse the process of encapsulation for recieved data.
* **TLD:** Top-Level Domain server, lower level servers whose work is to get request from DNS servers to manage it. Each TLD is relationated with an extension such as _.com_ and only manage request with its own stablished extension.
* **Authoritative name servers:** Get request from TLD servers, store DNS records for domains directly, send a response with the relevant information back to you, allowing connection to the IP address behind the domain requested.
* **TTL:** Time to Live, tells how much time the information of a request stored in local Cache is being considered valid, before asking answer to server again.
* **Port:** Constructs used to direct traffic to the right application on a server. There are 65535 ports available on every computer, and the fisrt 1024 of them are well-know being used for specific protocols.
* **RFC 793:** Norm that stablished de right behaviour for TCP protocol.
* **RFC 3912:** Norm that stablished de right behaviour for WHOIS protocol.
* **Ping Sweep:** Send an ICMP packet to each possible IP address for a specified network to map it.
* **CIDR:** Classless Inter-Domain Routing, useful notation for identifying subnets. It takes Ip adress and add netmask at the final of address as _/mask_.  **Ex**: _192.168.34.23/24_ for the mask _255.255.255.0_
* **TUN:** Abreviation for TUNnel, simulates a network layer device and operates in layer 3 carrying IP packets.
* **SSID:** Service Set Identifier, name given to a network to recognized from another networks near by.
* **Firewall:** Look deeper into a network traffic and identify malicious behavior to blocked.
  * **Network layer:** Filters communications based on source and destination IP addresses.
  * **Transport layer:** Filters communications based on source and destination data ports, as well as connection states.
  * **Aplication layer:** Filters communications based on an application, program or service.
  * **Context Aware layer:** Filters communications based on the user, device, role, application type and threat profile.
  * **Proxy:** Filters web content requests like URLs, domain names and media types.
  * **Reverse proxy:** Placed in front of web servers, reverse proxy servers protect, hide, offload and distribute access to web servers.
  * **NAT:** Network Acces Translation, hides or masquerades the private addresses of network hosts.
  * **Host-Based:** Filters ports and system service calls on a single computer operating system.
* **VPN:** Create a tunnel through the conection to a network where data is encrypted.
* **Antivirus:** Uses signatures or behavioral analysis of applications to identify and block malicious code.
* **NTLM:** New Technology Lan Manager, collection of authentication protocols as a challenge-response used to authenticate a client to a resource on an Active Directory domain.
