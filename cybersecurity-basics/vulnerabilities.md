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

# Vulnerabilities

A **vulnerability** is a weakness or flaw in the design, or implementation of a system or application that could be exploited by an attacker to compromise its security.&#x20;

<figure><img src="../.gitbook/assets/image (12) (1).png" alt="" width="320"><figcaption></figcaption></figure>

Vulnerabilities can arise from a variety of sources, such as poor coding practices, outdated software, misconfigurations, lack of encryption, or weak access controls. When left unaddressed, these weaknesses can allow attackers to gain unauthorized access, execute malicious code, escalate privileges, steal sensitive data, or disrupt services.

## <mark style="color:blue;">Types of Vulnerabilities</mark>

Vulnerabilities are often categorized based on their nature and the type of threat they pose. Here are some common types of vulnerabilities:

* **Segmentation Flaw:** Vulnerability due to connecting different functions of a network all in one, letting access to all network devices from other unrelated paths
* **Repudiation:** When an application or system does not adopt controls to properly track and log users' actions
* **IDOR:** Insecure Direct Object References, when an application uses user-supplied input to access objects directly. Affects the system because the web application does not validate whether the user has permission to access the requested object
* **Buffer Overflow:** Data is written or changed beyond the limits of a buffer (memory for an application) provoking the application to access memory allocated to other processes or crash
* **Non-Validated Input:** Data that the application isn't capable of processing is inserted which could cause crashing or malfunction
* **Race conditions:** The output of an event depends on ordered or timed outputs and it doesn't occur in the correct order or at the proper time
* **Version disclosure:** Show the version of the components used on a web page or application

## <mark style="color:blue;">CVEs</mark>

**Common Vulnerabilities and Exposures** is a standard to identify and categorize known vulnerabilities. They follow the structure _CVE-YEAR-IDNUMBER._ For example, the _CVE-2017-0144_ is associated with the famous exploit _Etenalblue._

There are some sources where people can access these reported vulnerabilities, or know how they are measured and categorized. Here are some of them:

* [**CVE&#x20;**_**Mitre**_](https://www.cve.org/)**:** Provides a reference system for publicly known information security vulnerabilities and exposures
* [**NVD**](https://nvd.nist.gov/vuln/search)**:** The National Vulnerability Databas&#x65;**,** managed by [_NIST_](https://www.nist.gov/), is a comprehensive database of vulnerability information, primarily based on CVE entries
* [**CVSS Calculator**](https://www.first.org/cvss/calculator/4.0)**:** Online tool that helps to calculate the Common Vulnerability Scoring System (CVSS) score for a given vulnerability
* [_**NIST**_**&#x20;CVSS Calculator:**](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator) Provided by _NIST_, enables users to calculate CVSS scores for vulnerabilities, offering a standardized approach to evaluating the potential impact of vulnerabilities
* [**CVEdetails**](https://www.cvedetails.com/)**:** Aggregates and displays information on CVEs, providing a detailed breakdown of the vulnerability, and being a useful tool for analyzing security risks and trends across different software and hardware products
