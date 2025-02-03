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

# Redeemer (Tier 0)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 0
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Redis / Vulnerability Assessment / Databases / Reconnaissance\
  &#x20;             / Anonymous-Guest Access

<figure><img src="../../.gitbook/assets/image (22) (1) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=0">https://app.hackthebox.com/starting-point?tier=0</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p- -Pn --min-rate 2000 10.129.136.187
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (105) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the first questions

<figure><img src="../../.gitbook/assets/image (87) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**6379**_



***

<figure><img src="../../.gitbook/assets/image (91) (1).png" alt=""><figcaption></figcaption></figure>

> Answe: _**redis**_

***

<figure><img src="../../.gitbook/assets/image (92) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**In-memory Database**_

***

<figure><img src="../../.gitbook/assets/image (93) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**redis-cli**_

***

<figure><img src="../../.gitbook/assets/image (99) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-h**_

***

<figure><img src="../../.gitbook/assets/image (100) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**info**_

***

* Then I did an exhaustive scan to get more information about the service running on the found port

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p6379 -sVC 10.129.136.187
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (106) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (101) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**5.0.7**_

***

<figure><img src="../../.gitbook/assets/image (102) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**select**_

***

* I found a [_Redis_](https://redis.io/) database, so I tried to get access to the database using the [_redis-cli_](../../database-attacks/tools-and-utilities.md#redis) utility and it worked successfully. Then, To get information about the database, I used the internal `info` command and got information from some of the keys that were configured

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>redis-cli -h 10.129.136.187
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (110) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (111) (1).png" alt=""><figcaption><p>This result is snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (112) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (107) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**4**_

***

<figure><img src="../../.gitbook/assets/image (108) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**keys \***_

***

* I selected the index of the database to work with it, in this case _0_ because the database name was _db0_ and was the first liste&#x64;_._ Then, I listed the keys using the `keys` and specifying to select all of them

<figure><img src="../../.gitbook/assets/image (113) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (114) (1).png" alt=""><figcaption></figcaption></figure>

***

* I found an interesting entry named _flag_ so I used the internal `get` command to retrieve its content and with this, I found the root flag

<figure><img src="../../.gitbook/assets/image (115) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (109) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**03e1d2b376c37ab3f5319922053953eb**_
