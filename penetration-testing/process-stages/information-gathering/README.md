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

# Information Gathering

Is the process of collecting as much publically accessible information about a target/organization as possible to obtain a deeper vision of the objective and possibly find vulnerable entry points.

<figure><img src="../../../.gitbook/assets/image (49).png" alt="" width="375"><figcaption></figcaption></figure>

In this process we can find two primordial steps:

* **Reconnaissance:** Preliminary survey to gather information about a target. It can be done in two ways:
  * **Passive:** Rely on publicly available knowledge, and access from publicly available resources without directly engaging with the target.
    * Looking up DNS records of a domain from a public DNS server.
      * Checking job ads related to the target website.
      * Reading news articles about the target company.
  * **Active:** Requires direct engagement with the target.
    * Connecting to one of the company servers such as HTTP, FTP, and SMTP.
      * Calling the company in an attempt to get information (social engineering).
      * Enter to physical centers of the target company.
* **Enumeration:** Extracting a system's information such as valid usernames, machine names, network resources, share names, directory names, and others.
