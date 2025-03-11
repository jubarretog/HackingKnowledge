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

# Enumeration

Involves systematically gathering information about a target's network, systems, and applications, focusing on extracting detailed data such as user accounts, network shares, open ports, and system settings, which can be leveraged to gain further access.

It is also done after gaining access to a shell in the target machine in the exploitation phase, which is named internal enumeration.

The resources we could look for are organized into three principal categories:

* **OS-based:** OS type, configuration files, sensitive files, network interfaces and configuration, users, groups, permissions, privileges, restrictions, environment variables, kernel info, hidden files
* **Host-based:** Processes, tasks, sources and destinations, accessible services, ports, protocols, version and configuration
* **Infrastructure-based:** Firewalls, proxies, IDS/IPS, EDR, VPN, Cloudflare, domains and subdomains, IP addresses, cloud instances, NetBlocks
