# Cyberattacks

A **cyberattack** refers to any deliberate attempt by an individual or group to compromise the confidentiality, integrity, or availability of information, systems, or networks.

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

Cyberattacks can range from highly targeted, sophisticated intrusions to broad, automated attacks, and they can be driven by various motives, such as financial gain, espionage, activism, or even sabotage.

<figure><img src="../../.gitbook/assets/image (941).png" alt="" width="457"><figcaption></figcaption></figure>

An attack arises from the notion that a target system stores or processes something valuable (objective), which leads attackers to test various tools and attack techniques (methods) to explore and exploit a weakness in the system (vulnerability) to fulfill their motives.

## <mark style="color:blue;">Attack Stages</mark>

Normally, attacks follow a specific flow with phases that an attacker goes through to successfully execute an attack. A possible way to generalize the principal stages is:

* **Information Gathering:** Collecting as much publicly accessible information about a target/organization as possible
* **Enumeration:** Discovering applications and services running on the systems
* **Exploitation:** Leveraging vulnerabilities discovered on a system or application
* **Privilege Escalation:** Attempt to expand the access and privileges on a system
* **Post-exploitation:** After getting access, we perform pivoting, obtain additional information, cover access tracks, and report vulnerabilities

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
* **Tampering:** The Action of manipulating a system by making changes to data that you should not, trying to damage and deteriorate it
* **Brute-Forcing:** Attack based on trying all the possible combinations till finding one that gains access to a system
* **DoS:** Denial of Service attack, causing the services can't be used by legitimate users in part or the entire network
  * **Reflected DoS:** Use another target as an intermediary, sending the packets first to this, and then this last sends the packets to perform the actual DoS attack
  * **Amplified DoS:** Attacks send packets where the response traffic is made up of packets that are much larger than those that were initially sent. Usually done by sending DNS queries to a DNS server, which replies with larger packets to the victim
  * **DDoS:** Distributed Denial of Service attack, originates from multiple, coordinated sources to generate a massive DoS attack
  * **Botnet:** A network of infected computers coordinated to launch DDoS attacks, distribute spam emails, or execute brute-force password attacks
* **MITM:** Man In The Middle, the attacker can get, insert, and modify data in the communication between two machines of a network. Consists of message interception without getting detected by a system
  * **MITMo:** Man In The Mobile, used to spy on application behavior, SMS, or voice calls from a phone, and relay back data to a hacker
* **Injection:** Insertion of packages, malicious or unauthorized code as part of their input in parts where the system shouldn't accept it
* **Living Off The Land:** Use built-in system tools and utilities with scripts or malicious code inserted, in an attempt to go undetected by system security
* **Social engineering:** All techniques aimed at talking a target into revealing specific information or performing a specific action for illegitimate reasons
  * **Phishing:** When an attacker impersonates a trusted source to present a malicious link or attachment via email
    * **Spear Phishing:** Constructed in a very specific way and directly targeted at specific groups of individuals or companies, and has a background profiling process by the attacker
    * **Whaling:** Targets high-profile business executives and key individuals in a company, designed to look like critical business emails or emails from someone who has legitimate authority, either within or outside the company
    * **Vishing:** Voice phishing, carried out in a phone conversation where an attacker persuades the user to reveal private, financial, or external information
    * **Smishing:** SMS phishing uses text messages to send malware or malicious links to mobile devices
  * **Pharming:** A type of impersonation attack in which a threat actor redirects a victim from a valid website or resource to a malicious one that could appear as the valid site to the user. Usually done by compromising previously DNS servers of the target website
  * **Impersonation:** Also known as pretexting, when an attacker presents as someone else to gain access to information
  * **Piggybacking:** When an unauthorized person tags along with an authorized person to gain entry to a restricted area, usually with the person’s consent
    * **Tailgating:** Essentially the same as Piggybacking, with the difference that it occurs without the authorized person’s consent
  * **Dumpster diving:** When a person searches for private information in garbage and recycling containers from a company or person
  * **Shoulder surfing:** When someone obtains information such as personally identifiable information, passwords, and other confidential data by looking over a victim’s shoulder
  * **Badge cloning:** When an attacker clones a badge, card, or any other device used to access a building
  * **USB Drop Key:** Leaving malicious USB drives unattended or placing them in strategic locations with the objective that a user thinks the devices are lost and inserts them into their systems
* **SEO Poisoning:** Search Engine Optimization is used to improve a website to gain greater visibility. Poisoning the SEO systems pushes malicious sites higher up the ranks of search results
* **Sniffing:** Capturing packets sent to the network to identify unencrypted data or patterns that can be used to decipher it
* **Password Spraying:** Based on trying the most commonly used passwords and patterns, or using one password to attempt to authenticate with as many different user names as possible, hoping for one successful authentication
* **Rainbow Table:** Compares the hash of a password with those stored in a dictionary of precomputed hashes called a _rainbow table_
* **Cryptojacking:** Hiding on a device or server and using it to mine cryptocurrencies without the user's consent or knowledge
* **Watering hole:** A targeted attack that occurs when an attacker profiles websites that the intended victim accesses to possibly compromise them and inject malicious code designed to redirect the user to another site
* **DNS cache poisoning:** Manipulation of the DNS resolver cache through the injection of corrupted DNS data, to force the DNS server to send the wrong IP address to a user and redirect the victim to another IP
* **Pass-The-Hash Attack:** Use a password hash collected from a compromised system to log in to another client or server, instead of figuring out what the user’s password is
* **Kerberoasting:** Extract service account credential hashes from Active Directory to crack them
* **Jamming:** A wireless attack that disrupts communication by flooding a Wi-Fi frequency with interference, preventing devices from connecting or transmitting data
* **KARMA Attack:** Karma Attacks Radio Machines Automatically, involves creating a rogue AP and allowing an attacker to intercept wireless traffic to listen for the probe requests from wireless devices and intercept them to generate the same SSID
* **KRACK:** Key Reinstallation Attack, manipulating and replaying cryptographic handshake messages tricks a wi-fi WPA2 network into reinstalling an already-in-use key
* **Bluejacking:** Performed using Bluetooth with vulnerable devices in range to send unsolicited messages to a victim
* **Bluesnarfing:** Performed to obtain unauthorized access to information from a Bluetooth-enabled device, allowing remote access to the local files of the target
* **Clickjacking:** Use multiple transparent or opaque layers to induce a user into clicking on a web button or link that redirects to a malicious site
