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

# IPMI

**Intelligent Platform Management Interface** operates at the hardware level and is used for remote management and monitoring of servers. It allows administrators to control, monitor, and recover systems, acting as an autonomous subsystem and working independently of the host's BIOS, CPU, firmware, and underlying operating system

It typically runs on UDP port 623 in the Application layer and provides low-level access to server hardware, enabling tasks such as power control, system monitoring, and troubleshooting, even if the system is powered off or unresponsive.

Its main uses are:

* Remote upgrades to systems without requiring physical access to the target host
* Modify BIOS settings before the OS has booted
* When the host is fully powered down or to access it after a system failure

Its main components are:

* **Baseboard Management Controller (BMC):** A micro-controller, essential component
* I**ntelligent Chassis Management Bus (ICMB):** An interface that permits communication from one chassis to another
* **Intelligent Platform Management Bus (IPMB):** Helps to extend the BMC
* **IPMI Memory:** Stores things such as the system event log, repository store data, and more
* **Communications Interfaces:** Local system interfaces, serial and LAN interfaces, ICMB and PCI Management Bus
