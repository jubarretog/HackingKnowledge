# Reporting

Reporting is a critical component that transforms technical activities and findings into a structured document, clearly communicating the assessment results to both technical and non-technical stakeholders.

A well-crafted report should detail the vulnerabilities discovered during the engagement, including how they were identified, the techniques used to exploit them, and the potential impact they could have on the organization’s assets, providing a basis for decision-making and even remediations to each vulnerability.

The report generally includes the following sections:

* **Statement of Confidentiality:** Outlines the confidentiality of the report and its contents, specifying that the report contains sensitive security details and should not be distributed or disclosed without prior consent
* **Engagement Contacts:** Lists the primary points of contact for both the client and the penetration testing team, including names, roles, email addresses, and phone numbers
* **Executive Summary**: A non-technical overview of the findings, suitable for management and decision-makers. Also describes the scope, methodology, and a summary of the findings (Ordered by severity)
* **Assessment Reproducibility:** A detailed walkthrough of how the assessment was done, the tools and techniques used, including all the steps and evidence from the start to the exploitation and beyond. Can also include topological diagrams
* **Remediation Summary:** Outlines areas of concern and provides actionable steps to mitigate the identified risks and correct the most significant security issues
* **Technical Findings Details**: Detailed technical breakdown of each vulnerability or misconfiguration, including:
  * **Description:** A clear explanation of the issue and how it was discovered
  * **Risk rating:** Includes a severity rating using CVSS, CWE, and CVSS Vector String
  * **Affected components:** Specifies which systems, applications, endpoints, or environments are impacted
  * **Impact:** Outlines the potential consequences if the issue is exploited
  * **Evidence:** Screenshots, logs, payloads, or POCs to support the finding
  * **Remediation Recommendations:** Specific, actionable steps to fix or mitigate the issue

The report serves as a roadmap for strengthening the organization’s security posture. It is often followed by a debriefing meeting with relevant stakeholders to discuss the findings, clarify any questions, and offer strategic guidance for remediation and future assessments.
