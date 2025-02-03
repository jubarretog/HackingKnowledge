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

# Meow (Tier 0)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 0
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Telnet / Protocols / Reconnaissance / Weak Credentials / Misconfiguration

<figure><img src="../../.gitbook/assets/image (19) (1) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=0">https://app.hackthebox.com/starting-point?tier=0</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* With a little research, I started answering the first questions&#x20;

<figure><img src="../../.gitbook/assets/image (27) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Virtual Machine**_

***

<figure><img src="../../.gitbook/assets/image (28) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Terminal**_

***

<figure><img src="../../.gitbook/assets/image (29) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**openvpn**_

***

<figure><img src="../../.gitbook/assets/image (30) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ping**_

***

<figure><img src="../../.gitbook/assets/image (31) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**nmap**_

***

* Then I continued doing an initial port scan of the machine using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.54.192 -p- -Pn --min-rate 2000
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (24) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (32) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**telnet**_

***

* Then I did an exhaustive scan to get information on the services running on the found ports

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.54.192 -p23 -sVC
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (25) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

* I found a port running the Telnet protocol, so I tried to connect through this protocol using common credentials. When using _root_ as username to log in, fortunately, gained access without being asked for a password

{% code lineNumbers="true" %}
```bash
telnet 10.129.54.192
```
{% endcode %}

<div align="center" data-full-width="false"><figure><img src="../../.gitbook/assets/image (33) (1) (1).png" alt=""><figcaption></figcaption></figure></div>

<figure><img src="../../.gitbook/assets/image (38) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the Telnet protocol, you can go [here](../../networks/protocols/telnet.md)
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (37) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**root**_

***

* Once inside, I checked the files in the folder I was in and found a _flag.txt_ file, that when reading its content gave me the root flag

<figure><img src="../../.gitbook/assets/image (41) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (40) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (39) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**b40abdfe23665f766f9c61ecba8a4c19**_
