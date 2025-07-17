# SNMP

**Simple Network Management Protocol** operates on UDP ports 161/162 in the Application layer. It is used for monitoring and managing network devices such as routers, switches, servers, printers, and IoT devices.

It helps in remote monitoring by collecting device statistics like CPU usage, memory, and network traffic, allows remote configuration and troubleshooting of network devices, and alerts administrators about critical issues.

This protocol has 3 versions being the version 1, the most vulnerable to enumeration and attacks in general.

&#x20;It operates in a client-server model in the following way:

* &#x20;The central system that requests and collects data from network devices is called the _SNMP Manager_
* The network devices that run software to collect and report data to the _SNMP Manager_ are called _SNMP Agents_
* A database structure defining what information can be monitored and managed is called a _Management Information Base (MIB)_
* To communicate, it uses petitions sent across the network. There are:
  * **GET:** The SNMP Manager asks for information from an SNMP Agent
  * **SET:** The SNMP Manager changes a setting on a device
  * **TRAP:** An SNMP Agent sends an alert to the SNMP Manager
  * **WALK:** Retrieves multiple pieces of information at once
