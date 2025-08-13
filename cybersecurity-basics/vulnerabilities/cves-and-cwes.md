# CVEs and CWEs

**Common Vulnerabilities and Exposures (CVEs)** is a standard to identify and categorize known vulnerabilities. They follow the structure _CVE-YEAR-IDNUMBER._ For example, _CVE-2017-0144_ is associated with the famous exploit _EternalBlue._

On the other side, **Common Weakness Enumeration (CWE)** is a list and classification system for software weaknesses and vulnerabilities. Unlike CVE, which identifies specific vulnerabilities, CWE focuses on the underlying types of software flaws that can lead to exploitable vulnerabilities. They follow the structure _CWE-IDNUMBER_ and a structured description of the weakness, common consequences, and recommended mitigations.

## <mark style="color:blue;">CVSS</mark>

The **Common Vulnerability Scoring System** is an industry standard for categorizing the severity associated with an issue, calculating a score that consists of the exploitability and impact of an issue. This calculation is based on three principal groups of metrics:

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p><a href="https://www.first.org/cvss/v3-1/media/MetricGroups.svg">https://www.first.org/cvss/v3-1/media/MetricGroups.svg</a></p></figcaption></figure>

* **Base Metric Group:** Represents the vulnerability characteristics and consists of exploitability metrics, which are a way to evaluate the technical means needed to exploit the issue, and impact metrics, which represent the repercussions of successfully exploiting an issue and what is impacted in an environment based on the CIA triad
* **Temporal Metric Group:** Details the availability of exploits or patches regarding the issue. Consists of the exploit code maturity, which represents the probability of an issue being exploited based on ease of exploitation techniques, the remediation level used to identify the prioritization of a vulnerability, and the report confidence represents the validation of the vulnerability and how accurate the technical details of the issue are
* **Environmental Metric Group:** Represents the significance of the vulnerability of an organization, taking into account the CIA triad. It uses the modified base metrics, which represent the metrics that can be altered if the affected organization deems a more significant risk in confidentiality, integrity, and availability to their organization

## <mark style="color:blue;">Sources</mark>

There are some sources where people can access reported vulnerabilities or learn how they are measured and categorized. Here are some of them:

* [**CVE&#x20;**_**Mitre**_](https://www.cve.org/)**:** Provides a reference system for publicly known information security vulnerabilities and exposures
* [**CWE&#x20;**_**Mitre**_](https://cwe.mitre.org/)**:** Offers detailed descriptions, taxonomies, and categorizations of software weaknesses, including example code, mitigation strategies, and relationships among weaknesses.
* [**NVD**](https://nvd.nist.gov/vuln/search)**:** The National Vulnerability Databas&#x65;**,** managed by [_NIST_](https://www.nist.gov/), is a comprehensive database of vulnerability information, primarily based on CVE entries
* [**CVSS Calculator**](https://www.first.org/cvss/calculator/4.0)**:** An online tool that helps to calculate the Common Vulnerability Scoring System (CVSS) score for a given vulnerability
* [_**NIST**_**&#x20;CVSS Calculator:**](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator) Provided by _NIST_, enables users to calculate CVSS scores for vulnerabilities, offering a standardized approach to evaluating the potential impact of vulnerabilities
* [**CVEdetails**](https://www.cvedetails.com/)**:** Aggregates and displays information on CVEs, providing a detailed breakdown of the vulnerability, and is a useful tool for analyzing security risks and trends across different software and hardware products
* [**CAPEC**](https://capec.mitre.org)**:**  Common Attack Pattern Enumeration and Classification is a public database of known attack patterns maintained by [_MITRE_](https://www.mitre.org)_._ Provides documents about how attackers exploit software weaknesses, offering a structured way to describe attack patterns
