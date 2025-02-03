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

# Process Stages

Penetration Testing is a methodical process that follows distinct stages to ensure thorough identification and analysis of security vulnerabilities.

To take a look at the bigger picture, we can observe the following diagram that describes the process:

<figure><img src="../../.gitbook/assets/image (53) (1).png" alt=""><figcaption><p><a href="https://academy.hackthebox.com/module/90/section/1569">https://academy.hackthebox.com/module/90/section/1569</a></p></figcaption></figure>

Here we can find 8 main stages that define the entire process of Penetration Testing, which are not always sequential:

* **Pre-Engagement:** The commitments, tasks, scope, limitations, and related agreements are set and documented in writing. It could contain Non-Disclosure agreements, goals, scope, time estimation, and Rules of Engagement.
* **Information Gathering:** Collecting as much publically accessible information about a target/organization as possible.
* **Vulnerability Assessment:** Use of the information found to identify potential weaknesses. We use vulnerability scanners and do manual analysis to discover where a potential security breach might lie.
* **Exploitation:** Perform an attack against a system based on potential vulnerabilities we have found before. The two main areas covered are network exploitation and web exploitation.
* **Post-Exploitation:** Do an examination and information gathering from the inside, and then study if is possible to do a privilege escalation and gain full-access control of the system.
* **Lateral Movement:** Also known as Pivoting, leverage the privileges or gaps to move through the network. We can use it to overlap with other internal hosts and further escalate our privileges within the current subnet or another part of the network.
* **Proof of Concept (PoC):** Any technique, tool, or script that demonstrates the exploitation of a vulnerability. Are sent along with the documentation allowing administrators to use them to confirm the issues themselves.
* **Post-Engagement:** Includes the documentation and reporting process, and also cleaning up the systems we exploit so that none of these systems can be exploited using our tools.
