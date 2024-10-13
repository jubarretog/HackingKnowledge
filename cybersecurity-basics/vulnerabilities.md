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

<figure><img src="../.gitbook/assets/image (12).png" alt="" width="320"><figcaption></figcaption></figure>

Vulnerabilities can arise from a variety of sources, such as poor coding practices, outdated software, misconfigurations, lack of encryption, or weak access controls. When left unaddressed, these weaknesses can allow attackers to gain unauthorized access, execute malicious code, escalate privileges, steal sensitive data, or disrupt services.

## <mark style="color:blue;">Types of Vulnerabilities</mark>

Vulnerabilities are often categorized based on their nature and the type of threat they pose, such as:

* **Segmentation Flaw:** Vulnerability due to connecting different functions of a network all in one, letting access to all network devices from other unrelated paths.
* **Repudiation:** When an application or system does not adopt controls to properly track and log users' actions.
* **IDOR:** Insecure Direct Object References, when an application uses user-supplied input to access objects directly. Affects the system because the web application does not validate whether the user has permission to access the requested object.
* **Buffer Overflow:** Data is written or changed beyond the limits of a buffer (memory for an application) provoking the application to access memory allocated to other processes or crash.
* **Non-Validated Input:** Data that the application isn't capable of processing is inserted which could cause crashing or malfunction.
* **Race conditions:** The output of an event depends on ordered or timed outputs and it doesn't occur in the correct order or at the proper time.
* **Version disclosure:** Show the version of the utilities used on a web page or application.

## <mark style="color:blue;">CVEs</mark>

**Common Vulnerabilities and Exposures** is a standard to identify and categorize known vulnerabilities.&#x20;

The CVEs follow the structure _CVE-YEAR-IDNUMBER._ For example, the _CVE-2017-0144_ is associated with the famous exploit _Etenalblue._

Some sources where we can access these reported vulnerabilities, or know how they are measured and categorized, are the following:

* **CVE Mitre:** Website that keeps track of CVEs [https://www.cve.org/](https://www.cve.org/)
* **NVD:** Vulnerabilities based on NIST framework [https://nvd.nist.gov/vuln/search](https://nvd.nist.gov/vuln/search)
* **CVSS Calculator:** [https://www.first.org/cvss/calculator/4.0](https://www.first.org/cvss/calculator/4.0)
* **NIST CVSS Calculator:** [https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator)
* **CVEdetails:** [https://www.cvedetails.com/](https://www.cvedetails.com/)
