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

# Meow

## <mark style="color:blue;">Description</mark>

* **Tier **<mark style="color:green;">**->**</mark> 0
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags **<mark style="color:green;">**->**</mark> Telnet / Protocols / Reconnaissance / Weak Credentials / Misconfiguration

<figure><img src="../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>



## <mark style="color:blue;">Write-up</mark>

* We start answering the first questions

<figure><img src="../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Virtual Machine**_

***

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Terminal**_

***

<figure><img src="../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

> Answer: _**openvpn**_

***

<figure><img src="../../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ping**_

***

<figure><img src="../../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

> Answer: _**nmap**_

***

* Then we continue making a initial port scan of the machine

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.54.192 -p- -Pn --min-rate 2000
</strong></code></pre>

<figure><img src="../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

***

* With this we can answer the next question

<figure><img src="../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

> Answer: _**telnet**_

***

* Now we can make an exhaustive scan

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.54.192 -p- -Pn --min-rate 2000
</strong></code></pre>

<figure><img src="../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

***

* We can try to connect through telnet protocol

{% code lineNumbers="true" %}
```bash
telnet 10.129.54.192
```
{% endcode %}

<div align="center" data-full-width="false">

<figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

</div>

***

* If we use _root_ as username to login we get access without being asked for password

<figure><img src="../../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

***

* With this we answer the next question

<figure><img src="../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Root**_

***

* We check the files in the directory

{% code lineNumbers="true" fullWidth="true" %}
```bash
ls
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

***

* We check the content of the _flag.txt_ file

```purebasic
cat flag.txt
```

<figure><img src="../../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

***

* With this we have got the root flag and have pawned the machine

<figure><img src="../../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

> Answer: _**b40abdfe23665f766f9c61ecba8a4c19**_
