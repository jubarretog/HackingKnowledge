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

# Categorization

Penetration testing can be categorized into different types based on the scope, knowledge, and methods used. Each type serves a unique purpose in assessing security from different perspectives, helping organizations strengthen their defenses by uncovering potential weaknesses under varying conditions.

## <mark style="color:blue;">Testing Methods</mark>&#x20;

These define the perspective/approach of the Penetration Test. Can be classified into two types:

* **External Penetration Test:** Performed as an anonymous user on the Internet or without direct access to the company network, to ensure that have protection against attacks on the external network perimeter. The principal goal is to access external-facing hosts, obtain sensitive data, or gain access to the internal network
* **Internal Penetration Test:** We perform testing from within the corporate network. This could be done after successfully gaining access to the internal network or starting from an assumed breach scenario where we can access isolated systems with no internet access

## <mark style="color:blue;">Types of Pen-Testing</mark>&#x20;

The penetration testing process can be cataloged based on the information given at the start of the testing. We can find three categories for this:&#x20;

<figure><img src="../.gitbook/assets/image (259) (1).png" alt=""><figcaption><p><a href="https://www.shakebugs.com/blog/black-vs-white-vs-grey-box-testing/">https://www.shakebugs.com/blog/black-vs-white-vs-grey-box-testing/</a></p></figcaption></figure>

* **Blackbox:** We are only given essential information, such as IP addresses or domains
* **Greybox:** We are provided with additional information, such as specific URLs, hostnames, subnets, and similar. Is a middle point between Blackbox and Whitebox
* **Whitebox:** Everything is disclosed to us, where we have an internal view of the entire structure, detailed configurations, admin credentials, web application source code, etc. This allows us to prepare an attack using internal information

Also can be cataloged by the roles that the Pen-Tester assumes in the assessment:

<figure><img src="../.gitbook/assets/image (258) (1).png" alt=""><figcaption></figcaption></figure>

* **Red-Teaming:** This may include physical testing, social engineering, and any other attack technique. This simulates a real-world attack where there are no boundaries and everything is valid
* **Purple-Teaming:** It can be combined with any of the above types, but focuses on working closely with the defenders (The Blue Team) to discover and at the same time solve the security gaps

## <mark style="color:blue;">Types of Testing Environments</mark>

It usually refers to specific types of company activities or assets that are going to be involved in the penetration testing process. Between them we can find the following:

<figure><img src="../.gitbook/assets/image (260) (1).png" alt=""><figcaption><p><a href="https://academy.hackthebox.com/module/90/section/935">https://academy.hackthebox.com/module/90/section/935</a></p></figcaption></figure>
