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

# Attacks

An attack refers to any deliberate attempt by an individual or group to compromise the confidentiality, integrity, or availability of information, systems, or networks.

## <mark style="color:blue;">Attack Stages</mark>

* **Information Gathering:** Collecting as much publically accessible information about a target/organization as possible.
* **Enumeration:** Discovering applications and services running on the systems.
* **Exploitation:** Leveraging vulnerabilities discovered on a system or application.
* **Privilege Escalation:** Attempt to expand the access and privileges on a system.
* **Post-exploitation:** After getting access we perform pivoting, get additional information that can be gathered, cover the access tracks, and report the vulnerabilities.

## <mark style="color:blue;">Classification of attacks</mark>

* **Passive:** Is focused on monitoring and interception of data flows through network traffic.
* **Active:** Data tampering, corruption, extraction, or disruption of communication between secured systems.
* **Close-in:** The attacker is in close physical proximity to the objective target. Normally focused on gathering, modification, or disruption of access to a system's information.
* **Insider:** These are performed by trusted persons using privileged access to violate rules or intentionally cause a threat.
* **Distribution:** Tampering with hardware or software before installation.

## <mark style="color:blue;">Types of Attacks</mark>

* **Spoofing:** A networked device pretends to identify as another using its MAC address.
* **On-path:** Intercept or modify communications between two devices.
* **Tampering:** Action of manipulating a system by making changes to data that you should not, trying to damage and deteriorate it.
* **Brute-Forcing:** Attack based on trying all the possible combinations till finding one who gains access to a system.
* **DOS:** Denial Of Service attack, cause that services can't be obtained from legitim users in a part or the entire network.
* **DDOS:** Distributed Denial Of Service attack, originates from multiple, coordinated sources to generate a massive DOS attack.
* **MItM:** Man In The Middle, the attacker can get, insert, and modify data in the communication between two machines of a network. Consist in message interception without getting detected by a system.
* **MItMo:** Man In The Middle, can spy on application behavior, SMS, or voice calls from a phone and relay them back the data to the hacker.
* **XSS:** Cross-site scripting, consisting of the injection of JS-HTML-CSS code or other types of scripts from the client side.
* **Injection:** Insertion of packages, malicious or unauthorized code as part of their input in parts where the system shouldn't accept it.
* **Living Off The Land:** Use built-in system tools and utilities with scripts or malicious code inserted, in an attempt to go undetected by system security.
* **Social engineering:** All techniques aimed at talking a target into revealing specific information or performing a specific action for illegitimate reasons.
* **Botnet:** A network of infected computers coordinated to launch DDoS attacks, distribute spam emails, or execute brute-force password attacks.
* **SEO Poisoning:** Search Engine Optimization, improving a website for gaining greater visibility. Poisoning pushes malicious sites higher up the ranks of search results.
* **Sniffing:** Capturing packets sent to the network to identify unencrypted data or patterns that can be used to decipher it.
* **Spraying:** This is based on trying the most commonly used passwords and patterns. A dictionary can also be used for this technique.
* **Rainbow Table:** Compares the hash of a password with those stored in a dictionary of precomputed hashes called _rainbow table._
* **KRACK:** Key Reinstallation Attack, manipulating and replaying cryptographic handshake messages tricks a wi-fi WPA2 network into reinstalling an already-in-use key.
* **Cryptojacking:** Hiding on a device or server and using it to mine cryptocurrencies without the user's consent or knowledge.
