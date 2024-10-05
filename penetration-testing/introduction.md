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

# Introduction

Penetration Testing is the organized, targeted, and authorized process where we are allowed to perform actions against an IT infraestructure to detect vulnerabilities and security breaches in the system.&#x20;

In contrast to a penetration test, vulnerability or security assessments are performed using purely automated tools.

Since the first moment the scope of the assesment must be define. This scope could define network boundaries, assets we can interact with, tools and actions forbidden in the assessment, between others legal delimitation.

The most important thing is that we **must stay within this scope** in any action we perform, and also all of this must be documented and written explicitly before proceding.

To take a look at the bigger picture, we can observe the following diagram that describes the process:

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p><a href="https://academy.hackthebox.com/module/90/section/1569">https://academy.hackthebox.com/module/90/section/1569</a></p></figcaption></figure>

* **Pre-Engagement:** The commitments, tasks, scope, limitations, and related agreements are set and documented in writing.It could contain Non-Disclosure agreements, goals, scope, time estimation, and rules of Engagement.
* **Information Gathering:** Collecting as much publically accessible information about a target/organisation as possible.
* **Vulnerability Assessment:** Use of the information found to identify potential weaknesses. We use vulnerability scanners and do manual analysis to discover where a potential security breach might lie.
* **Exploitation:** Perform an attack against a system based on potential vulnerabilities we have found before. The two main areas covered are Network Explotation and [Broken link](broken-reference "mention").
* **Post-Explotation:** Do examination and information gathering from the inside, and then study if is possible to do a privilege escalation and gain full-access control of the system.
* **Lateral Movement:** Also known as Pivoting, leverage the privileges or gaps to move through the network. We can use it to overlap with other internal hosts and further escalate our privileges within the current subnet or another part of the network.
* **Proof of Concept (PoC):** Any technique, tool or script that demonstrates the exploitation of a vulnerability. Are sent along with the documentation allowing administrators to use them to confirm the issues themselves.
* **Post-Engagement:** Includes the documentation and reporting process, and also cleaning up the systems we exploit so that none of these systems can be exploited using our tools.



## <mark style="color:blue;">Testing Methods</mark>&#x20;

Define the perspective/approach of the Penetration Test

* **External Penetration Test:** Performed as an anonymous user on the Internet or without direct access to the company network, to ensure that have protection against attacks on the external network perimeter. The principial goal is to access external-facing hosts, obtain sensitive data, or gain access to the internal network.
* **Internal Penetration Test:** We perform testing from within the corporate network. Could be done after successfully gain access to the internal network or starting from an assumed breach scenario where we can access isolated systems with no internet access.

## <mark style="color:blue;">Types of Pen-Testing</mark>&#x20;

They can be cataloged by the information given at the start of the testing:

<figure><img src="../.gitbook/assets/image (259).png" alt=""><figcaption><p>Own Resource</p></figcaption></figure>

* **Blackbox:** We ar only given essential information, such as IP addresses or domains.
* **Greybox:** We are provided with additional information, such as specific URLs, hostnames, subnets, and similar. Is a middle point between Blackbox and Whitebox.
* **Whitebox:** Everything is disclosed to us, where we have an internal view of the entire structure, detailed configurations, admin credentials, web application source code, etc. This allows us to prepare an attack using internal information.

Also can be cataloged by the roles that the Pen-Tester assume in the assessment:

<figure><img src="../.gitbook/assets/image (258).png" alt=""><figcaption><p>Own Resource</p></figcaption></figure>

* **Red-Teaming:** May include physical testing,social engineering, and any other attack technique. This simulates a real world attack where there are no boundaries and all is valid.&#x20;
* **Purple-Teaming:** It can be combined with any of the above types, but focuses on working closely with the defenders (The Blue Team) to discover an at the same time solve the security gaps.



## <mark style="color:blue;">Types of Testing Environments</mark>

It usaully refers to specific types of company actives

<figure><img src="../.gitbook/assets/image (260).png" alt=""><figcaption><p><a href="https://academy.hackthebox.com/module/90/section/935">https://academy.hackthebox.com/module/90/section/935</a></p></figcaption></figure>



## <mark style="color:blue;">Legal Documents</mark>

For the pre-engagement process is neccesary to estipulate all parameters in writing. Some of the usual documents we found for this puposes are the following:

* **NDA:** Non-Disclosure Agreement: Specifies the boundaries about the confidentiality and permissions to share the information received with third parties.
* **Scoping Questionnaire:** Defines the services we are going to provide to the client.
* **Scoping Document:** Summarize the information of the Scoping Questionnaire.
* **SoW:** Scope of Work or Penetration Testing Proposal, usually the contract that specifies the actions and scope of the assessment.
* **RoE:** Rules of Engagement, document that is created at the initial stages of a penetration testing engagement. This document consists of three main sections:
  * _Permissions:_ Give explicit and legal permission for the engagement to be carried out.
  * _Test Scope:_ Annotate specific targets of a network to which the engagement should apply.
  * _Rules:_ Define exactly the techniques that are permitted during the engagement.
* **Contractors Agreement:** Used in physical and social engineering testing to justify our actions.
* **Reports:** Summaries all the information after done the Pen-Testing.

