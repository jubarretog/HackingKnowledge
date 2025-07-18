# Related Concepts

* **NIC:** Network Interface Card, a hardware component that enables a computer or device to connect to a network, allowing communication over wired or wireless connections
* **Routing:** The Process of data traveling through a network
* **ISP:** Internet Service Provider, a company or organization that provides access to the Internet for individuals, businesses, and other entities
* **Public address:** Used to identify the device on the Internet, is given by the ISP
* **Private address:** Used to identify a device amongst other devices
* **MAC address:** Media Access Control is a hardware address set by the manufacturer in network interface cards. It's a twelve-character hexadecimal number. The first six characters represent the company that made the network interface, and the last six are unique numbers
* **IP address:** Internet Protocol address, identifies a host on a network and can't be active simultaneously more than once within the same network. It's formed by 4 octets of bits, each octet represents a number in the range 0-255
* **LAN:** Local Area Network
* **Ping:** A way to send ICMP packets to determine the performance of a connection between devices
* **SCP:** Secure File Copy, transfer files between two computers using the SSH protocol to provide authentication and encryption
* **Switch:** A device designed to aggregate multiple other networking-capable devices using Ethernet. Sends the package only to the intended target, thus reducing network traffic
* **Repeaters:** Have the same function as the switch but replay the sent information to all devices connected to it
* **Router:** Connects networks and passes data between them
* **Network Address** Identifies the start of the actual network
* **Host Address:** Used to identify a device on the subnet
* **Default Gateway:** A special address assigned to a device on the network that is capable of sending information to another network
* **Encapsulation:** The process of data getting added information details as it goes through every layer before getting sent
* **De-Encapsulation:** Reverse the process of encapsulation for received data
* **TLD:** Top-level Domain server, lower-level servers whose work is to get requests from DNS servers to manage them. Each TLD is related to an extension, such as _.com,_ and only manages requests with its own established extension
* **Authoritative name servers:** Get requests from TLD servers, store DNS records for domains directly, and send a response with the relevant information back to you, allowing connection to the IP address behind the domain requested
* **TTL:** Time to Live, tells how much time the information of a request stored in the local cache is considered valid, before asking the server again for an answer
* **Port:** Constructs used to direct traffic to the right application on a server. There are 65535 ports available on every computer, and the first 1024 of them are well-known, used for specific protocols
* **RFC 793:** A Norm that establishes the right behavior for the TCP protocol
* **RFC 3912:** A Norm that establishes the right behavior for the WHOIS protocol
* **RFC 5322:** A Norm that establishes the right behavior for the SMTP protocol
* **Ping Sweep:** Send an ICMP packet to each possible IP address for a specified network to map it
* **CIDR:** Classless Inter-Domain Routing, a useful notation for identifying subnets. It takes the IP address and adds a netmask at the final part of the address\
  **Ex**: In _192.168.34.23/24,_ the _/24_ represents the mask _255.255.255.0_
* **TUN:** Abbreviation for TUNnel, simulates a network layer device and operates in the session layer, carrying IP packets
* **SSID:** Service Set Identifier, the name given to a network to be recognized from other networks nearby
* **Firewall:** Look deeper into network traffic and identify malicious behavior to block it
  * **Network layer:** Filters communications based on source and destination IP addresses
  * **Transport layer:** Filters communications based on source and destination data ports, as well as connection states
  * **Application layer:** Filter communications based on an application, program, or service
  * **Context-Aware layer:** Filter communications based on the user, device, role, application type, and threat profile
  * **Proxy:** Filters web content requests like URLs, domain names, and media types
  * **Reverse proxy:** Placed in front of web servers, reverse proxy servers protect, hide, offload, and distribute access to web servers
  * **NAT:** Network Address Translation hides or masquerades the private addresses of network hosts
  * **Host-Based:** Filters ports and system service calls on a single computer operating system
* **VPN:** Virtual Private Network, technology that establishes a secure connection between a user's device and a remote server by creating a tunnel where data is encrypted
* **Antivirus:** Uses signatures or behavioral analysis of applications to identify and block malicious code
* **NTLM:** New Technology Lan Manager, a collection of authentication protocols used as a challenge-response to authenticate a client to a resource on an Active Directory domain
* **Pivoting:** Use an already compromised machine to jump or get access to other machines on the same network
* **Tunneling:** Consists of encapsulating a network protocol over others to create an information tunnel on a computer network
* **NAC:** Network Access Control is a security system that ensures that only authorized and compliant devices are granted access to the network
  * **DAC:** Discretionary access control enables users to manage access to their resources by granting resource owners the responsibility of controlling access permissions.
  * **MAC:** Mandatory access control determines resource access based on the resource's security level and the user's security level or the process requesting access
  * **RBAC:** Role-based access control, users are assigned roles based on their job responsibilities or other criteria, and each role is granted a set of permissions
* **Monitoring:** Capturing, analyzing, and interpreting network traffic to identify security threats, performance issues, and suspicious behavior
* **Workgroup:** Is a LAN peer-to-peer network that can support a maximum of 10 hosts in the same subnet in _Windows_, and identifies an arbitrary collection of computers and their resources on an SMB network
* **LLMNR:** Link-Local Multicast Name Resolution is a network protocol that seeks to resolve computer names and/or domains on a LAN network, without requiring any configuration
* **CIFS:** Common Internet File System protocol is a cross-platform, transport-independent protocol that provides a mechanism for client systems to use file and print services made available by server systems over a network, considered a specific version of the SMB protocol
* **Relay server:** An SMTP server that is known, trusted, and verified by all others
* **Community strings:** Passwords used to determine whether the requested information can be viewed or not
