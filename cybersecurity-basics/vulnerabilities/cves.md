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

# CVEs

**Common Vulnerabilities and Exposures** is a standard to identify and categorize known vulnerabilities. They follow the structure _CVE-YEAR-IDNUMBER._ For example, the _CVE-2017-0144_ is associated with the famous exploit _Etenalblue._

There are some sources where people can access these reported vulnerabilities, or know how they are measured and categorized. Here are some of them:

* [**CVE&#x20;**_**Mitre**_](https://www.cve.org/)**:** Provides a reference system for publicly known information security vulnerabilities and exposures
* [**NVD**](https://nvd.nist.gov/vuln/search)**:** The National Vulnerability Databas&#x65;**,** managed by [_NIST_](https://www.nist.gov/), is a comprehensive database of vulnerability information, primarily based on CVE entries
* [**CVSS Calculator**](https://www.first.org/cvss/calculator/4.0)**:** Online tool that helps to calculate the Common Vulnerability Scoring System (CVSS) score for a given vulnerability
* [_**NIST**_**&#x20;CVSS Calculator:**](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator) Provided by _NIST_, enables users to calculate CVSS scores for vulnerabilities, offering a standardized approach to evaluating the potential impact of vulnerabilities
* [**CVEdetails**](https://www.cvedetails.com/)**:** Aggregates and displays information on CVEs, providing a detailed breakdown of the vulnerability, and being a useful tool for analyzing security risks and trends across different software and hardware products

## <mark style="color:blue;">CVSS</mark>

The **Common Vulnerability Scoring System** is an industry standard for categorizing the severity associated with an issue calculating a score that consists of the exploitability and impact of an issue. This calculation is based on three principal groups of metrics:

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p><a href="https://www.first.org/cvss/v3-1/media/MetricGroups.svg">https://www.first.org/cvss/v3-1/media/MetricGroups.svg</a></p></figcaption></figure>

* **Base Metric Group:** Represents the vulnerability characteristics and consists of exploitability metrics which are a way to evaluate the technical means needed to exploit the issue, and impact metrics which represent the repercussions of successfully exploiting an issue and what is impacted in an environment based on the CIA triad
* **Temporal Metric Group:** Details the availability of exploits or patches regarding the issue. Consists of the exploit code maturity which represents the probability of an issue being exploited based on ease of exploitation techniques, the remediation level used to identify the prioritization of a vulnerability, and the report confidence represents the validation of the vulnerability and how accurate the technical details of the issue are
* **Environmental Metric Group:** Represents the significance of the vulnerability of an organization, taking into account the CIA triad. It uses the modified base metrics which represent the metrics that can be altered if the affected organization deems a more significant risk in confidentiality, integrity, and availability to their organization
