# Core Protocols

Active Directory relies on several core protocols to perform functions related to authentication, authorization, replication, directory access, and resource discovery.

<figure><img src="../../.gitbook/assets/image (2).png" alt="" width="375"><figcaption></figcaption></figure>

We will give details of some of these protocols, and here we find a summary of their purposes:

* **Kerberos:** It's the default authentication protocol in Active Directory. It's based on tickets to provide mutual authentication and supports delegation
* **NTLM:** NT LAN Manager is a legacy authentication protocol, used when Kerberos isn’t available. It's less secure than Kerberos, being vulnerable to relay and brute-force attacks
* **LDAP:** Lightweight Directory Access Protocol is used to query and manage AD objects (users, groups, OUs, etc. It also has a secure version (LDAPS) that works over SSL/TLS
* **DRS:** The Directory Replication Protocol is used by Domain Controllers to synchronize changes in the directory. Runs over the Remote Procedure Call (RPC) protocol
* **DNS:** Domain Name System is essential for locating domain controllers and AD services, storing service location records. A dynamic version is also used (DDNS) to allow clients and DCs to update their DNS records automatically
* **SMB:** Server Message Block is a management and file sharing protocol used for file sharing, GPO delivery, and logon scripts
