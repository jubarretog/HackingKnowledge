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

A vulnerability is a weakness or flaw in the design, implementation of a system or application that could be exploited by an attacker.&#x20;

## <mark style="color:orange;">Types of Vulnerabilities</mark>

* **Segmentation Flaw:** Vulnerabilitie due to connect different functions of a network all in one, letting the access to all network devices from other unrelationated paths.
* **Repudiation:** When an application or system does not adopt controls to properly track and log users' actions.
* **IDOR:** Insecure Direct Object References, when an application uses user-supplied input to access objects directly. Affects system because the web application does not validate whether the user has permission to access the requested object.
* **Buffer Overflow:** Data is written or changed beyond the limits of a buffer (memory for an aplication) provoking the application to access memory allocated to other processes or crash.
* **Non-Validated Input:** Data that the aplication isn't capable to process is inserted wich could cause crashing or malfunctional.
* **Race conditions:** The output of an event depends on ordered or timed outputs and it don't occur in the correct order or at the proper time.
* **Cryptojacking:** Hiding on a device or server and using it to mine cryptocurrencies without the user's consent or knowledge.
* **Version disclosure:** Show the version of the utilities used on a web page or application.



## <mark style="color:orange;">CVEs</mark>

* Common Vulnerabilities and Exposures, is a standart for identify and categorize known vulnerabilities.&#x20;
* The CVEs follow the structure _CVE-$YEAR-$IDNUMBER_

### CVE Sources

* **CVE Mitre:** Website that keeps track of CVEs [https://www.cve.org/](https://www.cve.org/)
* **NVD:** Vulnerabilities based on NIST framework [https://nvd.nist.gov/vuln/search](https://nvd.nist.gov/vuln/search)
* **CVSS Calculator:** [https://www.first.org/cvss/calculator/4.0](https://www.first.org/cvss/calculator/4.0)
* **NIST CVSS Calculator:** [https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator)
* **Exploit DB:** retains exploits for software and applications [https://www.exploit-db.com/](https://www.exploit-db.com/)
* **Linux Kernel CVEs:** [https://www.linuxkernelcves.com/cves](https://www.linuxkernelcves.com/cves)

