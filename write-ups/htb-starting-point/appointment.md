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

# Appointment

## <mark style="color:blue;">Description</mark>

* **Tier **<mark style="color:green;">**->**</mark> 1
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags **<mark style="color:green;">**->**</mark> Databases / Apache / MariaDB / PHP / SQL / Reconnaissance / SQL Injection

<figure><img src="../../.gitbook/assets/image (117).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* We start

<figure><img src="../../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Structured Query Language**_

***

<figure><img src="../../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

> Anwer: _**SQL Injection**_

***

<figure><img src="../../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

> Answer: _**A03:2021 Injection**_

***

* We start doing an initial scan

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p- -Pn --min-rate 2000 10.129.228.241
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>

***

* Now we make an exhaustive scan

{% code lineNumbers="true" %}
```bash
nmap -p80 -sVC 10.129.228.241
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure>

***

* With this and some research, we can answer some question

<figure><img src="../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Apache httpd 2.4.38 ((Debian))**_

***

<figure><img src="../../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

> Answer: _**443**_

***

<figure><img src="../../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Directory**_

***

<figure><img src="../../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

> Answer: _**404**_

***

<figure><img src="../../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

> Answer: _**dir**_

***

<figure><img src="../../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

> Answer: _**#**_

***

* Now as we saw above, the HTTP service is running on port 80, meaning that there is a web page. We go and check it on the browser

<figure><img src="../../.gitbook/assets/image (136).png" alt=""><figcaption></figcaption></figure>

***

* As we see, there is a login form. We can assume that there is an SQL database checking the credentials for login and try a basic SQL Injection. If we try accessing with username _admin'#_ and any password, we gain access, and a message is displayed

<figure><img src="../../.gitbook/assets/image (137).png" alt=""><figcaption></figcaption></figure>

***

* With this, we can answer the following question

<figure><img src="../../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Congratulations**_

***

* And also, we have got the root flag and have pawned the machine.

<figure><img src="../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

> Answer: _**e3d0796d002a446c0e622226f42e9672**_
