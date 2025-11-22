---
layout:
  width: default
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
  metadata:
    visible: true
---

# Secure Design

By embedding security into the very foundation of system architecture and workflows, organizations can proactively identify and mitigate risks, reducing vulnerabilities and minimizing the impact of potential attacks.&#x20;

<figure><img src="../.gitbook/assets/image (926).png" alt="" width="310"><figcaption></figcaption></figure>

Building secure applications starts long before a single line of code is written; it begins at the design stage. The following principles guide teams in making informed, security-conscious decisions throughout the application development lifecycle:

* **Defense in Depth:** Security based on having multiple layers of defense that aim to eliminate or minimize vulnerable points, even if there are already other countermeasures in different layers
* **Fail Safe Defaults:** An application should preserve the availability, integrity, and confidentiality of information even when there are failures, and be able to revert to a previous safe state
* **Least Privilege:** Every user or process should have only the minimal permissions needed to perform their tasks. If necessary, elevated privileges should be assigned only temporarily
* **Separation of Duties:** Responsibilities should be divided so that no single individual has control over all parts of a critical process or workflow, establishing specific roles and permissions for distinct tasks
* **Economy of Mechanism:** Keep the architecture and processes as simple as possible, as simpler designs are easier to secure and maintain
* **Complete Mediation:** Never assume a previous authorization is still valid. Every access request should be revalidated, even if the user has already authenticated
* **Open Design:** Security should not depend on the secrecy of the design or implementation. Obscurity or hiding details is not a reliable form of protection
* **Psychological Acceptability:** Security features should be user-friendly and not overly intrusive. The more natural and transparent their use, the more effective they will be
* **Weakest Link:** An application’s security is defined by its weakest component. A single vulnerability in any one part can compromise the entire system
* **Leveraging Existing Components:** If there is already a tool, library, or component that solves a problem securely, use it, don’t reinvent the wheel or add unnecessary complexity
* **Secure by Default:** Applications should be secure as soon as they are deployed, with minimum exposure to risk
* **Protect Sensitive Data:** Sensitive information must be protected at all times, when stored, transmitted across networks, or displayed to users
* **Trace and Log:** All interactions with sensitive resources should be logged, including relevant audit events, ensuring traceability, supporting non-repudiation, and providing visibility in case of incidents
