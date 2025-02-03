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

# ARP

**Address Resolution Protocol** operates in the Data Link layer, and is used to map IP addresses to MAC addresses within a local network. It allows devices to find the hardware address of another device on the same subnet when only the IP address is known.

&#x20;It operates as follows:

* A request is sent to every other device in the network. This is known as _Broadcast_
* The device whose IP matches replies to the initial device with the MAC address
* The requesting device stores the result in its ARP cache for faster communication in the future
