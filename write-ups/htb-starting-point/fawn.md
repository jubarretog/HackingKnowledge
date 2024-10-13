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

# Fawn

## <mark style="color:blue;">Description</mark>

* **Tier **<mark style="color:green;">**->**</mark> 0
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags **<mark style="color:green;">**->**</mark> FTP / Protocols / Reconnaissance / Anonymous-Guest Access

<figure><img src="../../.gitbook/assets/image (20) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=0">https://app.hackthebox.com/starting-point?tier=0</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* We start answering the first questions

<figure><img src="../../.gitbook/assets/image (47) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**File Transfer Protocol**_

***

<figure><img src="../../.gitbook/assets/image (48) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**21**_

***

<figure><img src="../../.gitbook/assets/image (49) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**sftp**_

***

<figure><img src="../../.gitbook/assets/image (50) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ping**_

***

* Now we can make an initial port scan

{% code overflow="wrap" lineNumbers="true" %}
```sh
nmap -p- -Pn --min-rate 2000 10.129.92.84
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (46) (1).png" alt=""><figcaption></figcaption></figure>

***

* Then we make an exhaustive scan

{% code lineNumbers="true" %}
```bash
nmap -p- -Pn --min-rate 2000 10.129.92.84
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (52) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, we can answer the next four questions

<figure><img src="../../.gitbook/assets/image (51) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**vsftpd 3.0.3**_

***

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Unix**_

***

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ftp -h**_

***

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

> Answer: _**anonymous**_

***

* We try connecting through the FTP protocol

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>ftp 10.129.92.94
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

***

* We try login with the _anonymous_ user and entering a blank password

<figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

***

* With this, we can answer the next three questions

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

> Answer: _**230**_

***

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ls**_

***

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

> Answer: _**get**_

***

* We use the `ls` command to list files via FTP and we find a text file

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

***

* Now we use the _get_ command to pull the _flag.txt_ file via FTP and then we close the connection

<figure><img src="../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

***

* We check the content of the _flag.txt_ file

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

***

* With this, we have got the root flag and have pawned the machine.

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

> Answer: _**035db21c881520061c53e0536e44f815**_
