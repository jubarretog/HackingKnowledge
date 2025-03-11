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

# Synced (Tier 0)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 0
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Rsync / Protocols / Reconnaissance / Anonymous/Guest Access

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=0">https://app.hackthebox.com/starting-point?tier=0</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* With a little research, I started answering the first question

<figure><img src="../../.gitbook/assets/image (60) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**873**_

***

* Then I continued doing an initial port scan of the machine using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.197.128 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (68) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (59) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**1**_

***

* Then I did an exhaustive scan of the ports we found to get information about the running service

{% code lineNumbers="true" %}
```bash
nmap 10.129.197.128 -p873 -sVC -oN serv_scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (69) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered some questions

<figure><img src="../../.gitbook/assets/image (63) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: **31**

***

<figure><img src="../../.gitbook/assets/image (64) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**rsync**_

***

<figure><img src="../../.gitbook/assets/image (65) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**None**_

***

<figure><img src="../../.gitbook/assets/image (66) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**list-only**_

***

* I found there was a port a service named _rsync_ that with a little research, I found it was a file synchronization application. Also, I found that it was possible to interact with it using the [_rsync_](../../networks/tools-and-utilities.md#rsync) command-line utility. So I tried using it to list the files being shared under this application specifying it was using a daemon to run this service and I saw it was successful

{% code overflow="wrap" lineNumbers="true" %}
```bash
rsync --list-only 10.129.197.128::
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (70) (1).png" alt=""><figcaption></figcaption></figure>

***

* I found a _public_ folder so I listed its content where I found a _flag.txt_ file, so I transferred it from the server to my machine and read its content finally finding the root flag

{% code overflow="wrap" lineNumbers="true" %}
```bash
rsync --list-only 10.129.197.128::public
rsync 10.129.197.128::public/flag.txt ./
cat flag.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (39) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**72eaf5344ebb84908ae543a719830519**_
