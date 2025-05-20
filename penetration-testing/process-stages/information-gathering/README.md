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

<figure><img src="../../../.gitbook/assets/image (49) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

In this process we can find two primordial steps:

* **Reconnaissance:** Preliminary survey to gather information about a target. It is done in two ways:
  * **Passive:** Rely on publicly available knowledge, and access from publicly available resources without directly engaging with the target. Some actions that involve this are:
    * Checking job ads related to the target website
    * Reading news articles about the target company
    * Search Engine Queries
    * WHOIS/DNS Lookups
    * Web Archive Analysis
    * Social Media Analysis
    * Code Repositories
  * **Active:** Requires direct engagement with the target. Some actions that involve this are:
    * Port Scanning
    * Vulnerability Scanning
    * Network Mapping
    * Service Enumeration
    * Banner Grabbing
    * OS Fingerprinting
    * Web Spidering
    * Social engineering
    * Physical access
* **Enumeration:** Extracting as much system information as possible, such as valid usernames, machine names, network resources, share names, directory names, and others. Normally we scope this by some categories:
  * **Open-Source Intelligence:** Get as much public information as possible about the target
  * **Infrastructure enumeration:** Overview of the company's position on the internet and intranet. We use public services such as DNS to understand how the infrastructure is structured
  * **Service Enumeration:** Direct interaction with the assets, where we try to identify what version of a service is running, what information it provides us, and the reason it can be used
  * **Host Enumeration:** Identify the machines that are part of the infrastructure and the architecture they have internally, as well as the processes and services they run
