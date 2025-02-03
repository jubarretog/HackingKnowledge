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

# Cyberattacks

A **cyberattack** refers to any deliberate attempt by an individual or group to compromise the confidentiality, integrity, or availability of information, systems, or networks.

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt="" width="375"><figcaption></figcaption></figure>

Cyberattacks can range from highly targeted, sophisticated intrusions to broad, automated attacks, and they can be driven by various motives, such as financial gain, espionage, activism, or even sabotage.

## <mark style="color:blue;">Attack Stages</mark>

Normally, attacks follow a specific flow with phases that an attacker goes through to successfully execute an attack. A possible way to generalize the principal stages is:

* **Information Gathering:** Collecting as much publically accessible information about a target/organization as possible
* **Enumeration:** Discovering applications and services running on the systems
* **Exploitation:** Leveraging vulnerabilities discovered on a system or application
* **Privilege Escalation:** Attempt to expand the access and privileges on a system
* **Post-exploitation:** After getting access we perform pivoting, get additional information that can be gathered, cover the access tracks, and report the vulnerabilities

## <mark style="color:blue;">Classification of attacks</mark>

Attacks can also be categorized based on their impact or shape upon completion. Some common categories are:

* **Passive:** Is focused on monitoring and interception of data flows through network traffic
* **Active:** Data tampering, corruption, extraction, or disruption of communication between secured systems
* **Close-in:** The attacker is in close physical proximity to the objective target. Normally focused on gathering, modification, or disruption of access to a system's information
* **Insider:** These are performed by trusted persons using privileged access to violate rules or intentionally cause a threat
* **Distribution:** Tampering with hardware or software before installation

## <mark style="color:blue;">Types of Attacks</mark>

Also, the attacks are typically classified into different types based on their methods and goals. Some of these types are:

* **Spoofing:** A networked device pretends to identify as another using its MAC address
* **On-path:** Intercept or modify communications between two devices
* **Tampering:** Action of manipulating a system by making changes to data that you should not, trying to damage and deteriorate it
* **Brute-Forcing:** Attack based on trying all the possible combinations till finding one who gains access to a system
* **DOS:** Denial Of Service attack, cause that services can't be obtained from legitim users in a part or the entire network
* **DDOS:** Distributed Denial Of Service attack, originates from multiple, coordinated sources to generate a massive DOS attack
* **MItM:** Man In The Middle, the attacker can get, insert, and modify data in the communication between two machines of a network. Consist in message interception without getting detected by a system
* **MItMo:** Man In The Mobile, can spy on application behavior, SMS, or voice calls from a phone and relay back data to a hacker
* **Injection:** Insertion of packages, malicious or unauthorized code as part of their input in parts where the system shouldn't accept it
* **Living Off The Land:** Use built-in system tools and utilities with scripts or malicious code inserted, in an attempt to go undetected by system security
* **Social engineering:** All techniques aimed at talking a target into revealing specific information or performing a specific action for illegitimate reasons
* **Botnet:** A network of infected computers coordinated to launch DDoS attacks, distribute spam emails, or execute brute-force password attacks
* **SEO Poisoning:** Search Engine Optimization is used to improve a website for gaining greater visibility. Poisoning the SEO systems pushes malicious sites higher up the ranks of search results
* **Sniffing:** Capturing packets sent to the network to identify unencrypted data or patterns that can be used to decipher it
* **Password Spraying:** Based on trying the most commonly used passwords and patterns or using one password to attempt to authenticate with as many different user names as possible, hoping for one successful authentication
* **Rainbow Table:** Compares the hash of a password with those stored in a dictionary of precomputed hashes called _rainbow table_
* **KRACK:** Key Reinstallation Attack, manipulating and replaying cryptographic handshake messages tricks a wi-fi WPA2 network into reinstalling an already-in-use key
* **Cryptojacking:** Hiding on a device or server and using it to mine cryptocurrencies without the user's consent or knowledge
