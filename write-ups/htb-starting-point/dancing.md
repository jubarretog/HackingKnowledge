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

# Dancing

## <mark style="color:blue;">Description</mark>

* **Tier **<mark style="color:green;">**->**</mark> 0
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Windows
* **Tags **<mark style="color:green;">**->**</mark> Protocols / SMB / Reconnaissance / Anonymous-Guest Access

<figure><img src="../../.gitbook/assets/image (21) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=0">https://app.hackthebox.com/starting-point?tier=0</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* We start answering the first questions

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Server Message Block**_

***

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

> Answer: _**445**_

***

* Now we can make an initial port scan

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p- -Pn --min-rate 2000 10.129.76.14
</strong></code></pre>

<div data-full-width="false">

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

</div>

***

* With this, we can answer the next two questions

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

> Answer: _**microsoft-ds**_

***

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-L**_

***

* Now we make an exhaustive scan

{% code lineNumbers="true" %}
```bash
nmap -p135,139,445,5985,47001,49664,49665,49666,49667,49668,49669 -sVC 10.129.76.14
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

***

* We focus on port 445 which could have SMB protocol running. We try connecting using the _sbmclient_ tool to access the service and insert a blank password when prompted for it, With this we get a list of shares from the target machine.

{% code lineNumbers="true" %}
```bash
smbclient -L 10.129.76.14 
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

***

* Now we can answer the next question

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

> Answer: **4**

***

* Then we try accessing the shared folders. When we tried _WorkShares_, we gained access without being asked for a password

{% code lineNumbers="true" %}
```bash
smbclient //10.129.76.14/WorkShares
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

***

* Now we can answer the next two question

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

> Answer: _**WorkShares**_

***

<figure><img src="../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

> Answer: _**get**_

***

* Then we list the content of the shared folder with the `ls` command on the SMB command line

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

***

* If we go to the _James.P_ directory and list its content we can find a text file

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

***

* Now we use the _get_ command to pull the _flag.txt_ file from the SMB server and then we close the connection with it

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

***

* We check the content of the _flag.txt_ file

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

***

* With this, we have got the root flag and have pawned the machine.

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

> Answer: _**5f61c10dffbc77a704d76016a22f1664**_
