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

# Tools

## <mark style="color:green;">**Exploit DB**</mark>

* Retains exploits for software and applications
* [https://www.exploit-db.com/](https://www.exploit-db.com/)



## <mark style="color:green;">Searchsploit</mark>

* Kali package for acceding to exploitDB

### Commands

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install exploitdb
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
searchsploit $Keywords
```
{% endcode %}

***



## <mark style="color:green;">Metasploit</mark>&#x20;

Explotation framework with tools for every phase of pentesting

### Modules

* **Auxiliary:** Any supporting module.
* **Encoders:** Encode exploit and payload for bypassing signature-based antivirus.
* **Evasion:** For antivirus evasion.
* **Exploits:** Exploits, organized by target system.
* **Nops:** No OPeration, CPU will do nothing for one cycle, often used as a buffer to achieve consistent payload sizes.
* **Payloads:** Different payloads that can open shells on the target system.
  * **Adapters:** Convert single payloads into different formats.
  * **Single:** Also called _in-line_, do not need to download an additional component to run.
  * **Stagers:** Set up a connection channel between Metasploit and the target system, first the stager is uploaded on the target system then download the rest of the payload (stage).
  * **Stages:** Downloaded by the stage, allows to use larger sized payloads.
* **Post:** For post-explotation

{% hint style="info" %}
The difference between staged and single payloads is the use of `_` or `/` in notation

**Example:** `shell_reverse_tcp` (Single) ---`shell/reverse_tcp` (Staged) &#x20;
{% endhint %}

### Common parameters

* **RHOSTS:** IP address of the target system
* **RPORT:** Port on the target system the vulnerable application is running on.
* **PAYLOAD:** Payload that will use with the exploit.
* **LHOST:** Atacking machine (local) IP address.
* **LPORT:** Port (local) that will be uses for the reverse shell to connect back to.
* **SESSION:** Session ID od the connection eith metasploit. Used with post-exploitation modules connected to the target system.

### Commands

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install metasploit-framework
```
{% endcode %}

***

* Start metasploit console

{% code overflow="wrap" lineNumbers="true" %}
```bash
msfconsole
msf6\> sessions        #See all sessions
msf6\> session -i $id  #Change to a session
```
{% endcode %}

***

* List modules

{% code overflow="wrap" lineNumbers="true" %}
```bash
tree -L 1 /usr/share/metasploit-framework/modules        #Types
tree -L 1 /usr/share/metasploit-framework/modules/$type  #Specific module type
```
{% endcode %}

***

* Search module

{% code overflow="wrap" lineNumbers="true" %}
```bash
msf6\> search $query
msf6\> use $queryNumber #Use module from last search list (0 is the first)
msf6 > search type:$type $query #Filter by specific module type
```
{% endcode %}

{% hint style="info" %}
The _query_ can be a keyword, CVE number, exploit/module name or target system
{% endhint %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```sh
msf6\> use exploit/$exploit path
# This will enter in context of the exploit, below an example
msf6\> use exploit/windows/smb/ms17_010_eternalblue     #The exploit used
msf6 exploit(windows/smb/ms17_010_eternalblue)\>        #The terminal context set

'''\> info             #Display information about the module (''')
'''\> show options     #Display options for the actual context 
'''\> show payloads    #Display payloads that can be used with the exploit
'''\> show $module     #Can be used with every module type

'''\> set $parameter $value  #Set parameters in context
'''\> unset $parameter       #Unset a parameter
'''\> unset all              #Unset all parameters
'''\> setg $parameter $value #Set parameters globally
'''\> unsetg $parameter      #Unset global parameter

'''\> check       #Verify if vulnerable without exploiting
'''\> exploit     #Run exploit
'''\> run         #Same that exploit
'''\> exploit -z  #Run exploit and background session

'''\> background  #Background session, also CTLR+Z can be used

'''\> back             #Exit from context
```
{% endcode %}

***



## <mark style="color:green;">Payloads for Everything</mark>

* Repository that contains payloads for diverses purposes and attackas
* [https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master)



## <mark style="color:green;">LOLBAS</mark>

* Contain scripts, binaries and libraries for developing a Living off the Land attack
* [https://lolbas-project.github.io/](https://lolbas-project.github.io/)

