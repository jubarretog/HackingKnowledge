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

# Redeemer

## <mark style="color:blue;">Description</mark>

* **Tier **<mark style="color:green;">**->**</mark> 0
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags **<mark style="color:green;">**->**</mark> Redis / Vulnerability Assessment / Databases / Reconnaissance\
  &#x20;             Anonymous-Guest Access

<figure><img src="../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>



## <mark style="color:blue;">Write-up</mark>

* We start doing an initial scan

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p- -Pn --min-rate 2000 10.129.136.187
</strong></code></pre>

<figure><img src="../../../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

***

* With this we can answer the first questions

<figure><img src="../../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

> Answer: _**6379**_



***

<figure><img src="../../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

> Answe: _**redis**_

***

* With this we can answer the following questions

<figure><img src="../../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

> Answer: _**In-memory Database**_

***

<figure><img src="../../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

> Answer: _**redis-cli**_

***

<figure><img src="../../../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-h**_

***

<figure><img src="../../../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

> Answer: _**info**_

***

* Now we can make an exhaustive scan

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p6379 -sVC 10.129.136.187
</strong></code></pre>

<figure><img src="../../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

***

* With this we answer the next two questions

<figure><img src="../../../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

> Answer: _**5.0.7**_

***

<figure><img src="../../../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

> Answer: _**select**_

***

* Now we try to get access to the database using _redis-cli_&#x20;

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>redis-cli -h 10.129.136.187
</strong></code></pre>

<figure><img src="../../../.gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>

***

* To get information about the database we use `info` command on redis command line

<figure><img src="../../../.gitbook/assets/image (111).png" alt=""><figcaption><p>This result is snippet</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

***

* With this we can answer the next two questions

<figure><img src="../../../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

> Answer: _**4**_

***

<figure><img src="../../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

> Answer: _**keys \***_

***

* Now we select the index of the database, in this case _0_ as seen above (_db0_)

<figure><img src="../../../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>



s

***

* Now we list the keys using the `keys` command, to select all we use `*`

<figure><img src="../../../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>

***

* We can see a key named _flag_ so we use the `get` command to see its content

<figure><img src="../../../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

***

* With this we have got the root flag and have pawned the machine

<figure><img src="../../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

> Answer: _**03e1d2b376c37ab3f5319922053953eb**_
