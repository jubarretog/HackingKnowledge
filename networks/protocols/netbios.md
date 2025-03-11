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

# NetBIOS

**Network Basic Input/Output System**, is an IBM standard protocol that operates on the Session layer and allows applications on different computers to communicate within a local area network.&#x20;

This protocol provides three different services:

* **Name Service (NetBIOS-NS):** For name registration and resolution
* **Datagram Service (NetBIOS-DGM):** For connectionless communication
* **Session Service (NetBIOS-SSN):** For connection-oriented communication

Also, the NetBIOS operations use the following ports and protocols:

* Microsoft Remote Procedure Call (MS-RPC), which is an endpoint mapper used for client-to-client and server-to-client communication, on port 135
* NetBIOS Name Service, on UDP port 137
* NetBIOS Datagram Service, on UDP port 138
* NetBIOS Session Service, on port 139
* SMB protocol, used for sharing files between different operating systems, on port 445&#x20;
