---
hidden: true
---

# Active (Easy) (WIP)

## <mark style="color:blue;">Description</mark>

* **Difficult** <mark style="color:green;">**->**</mark> Easy
* **OS** <mark style="color:green;">**->**</mark> Windows
* **State** <mark style="color:green;">-></mark> Retired
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Vulnerability Assessment  &#x20;/ Enterprise Network / Active Directory  &#x20;/ Security Tools  \
  / Authentication  &#x20;/ Software & OS exploitation / Default Credentials  &#x20;/ Weak Permissions  \
  / Anonymous-Guest Access

<figure><img src="../../.gitbook/assets/image (944).png" alt="" width="451"><figcaption><p><a href="https://app.hackthebox.com/machines/Active">https://app.hackthebox.com/machines/Active</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started making an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap -p- -Pn --min-rate 2500 -oN scan.txt 10.129.189.118
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (945).png" alt="" width="563"><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to learn about the services running on the open ports

{% code lineNumbers="true" %}
```bash
nmap 10.129.93.176 -p22,80 -sVC -oN serv_scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (946).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (947).png" alt=""><figcaption></figcaption></figure>

***

* ;



***

* With that, I got the user flag

<figure><img src="../../.gitbook/assets/image (757).png" alt=""><figcaption></figcaption></figure>

> Answer: _**0ac28aeb5d1e8d1808cdd083961381ad**_

***

* A



***

* Finally, I navigated to the _/root_ folder where I found a _root.txt_ file, and reading its content, I got the root flag



***

* With that, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**8**_
