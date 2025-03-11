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

# Dancing (Tier 0)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 0
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Windows
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Protocols / SMB / Reconnaissance / Anonymous-Guest Access

<figure><img src="../../.gitbook/assets/image (21) (1) (1) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=0">https://app.hackthebox.com/starting-point?tier=0</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* With a little research, I started answering the first questions

<figure><img src="../../.gitbook/assets/image (68) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Server Message Block**_

***

<figure><img src="../../.gitbook/assets/image (69) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**445**_

***

* Then I did an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p- -Pn --min-rate 2000 10.129.76.14
</strong></code></pre>

<div data-full-width="false"><figure><img src="../../.gitbook/assets/image (71) (1) (1).png" alt=""><figcaption></figcaption></figure></div>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (70) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**microsoft-ds**_

***

<figure><img src="../../.gitbook/assets/image (72) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-L**_

***

* After this, I did an exhaustive scan to get information on the services running on the open ports

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -p135,139,445,5985,47001,49664,49665,49666,49667,49668,49669 -sVC 10.129.76.14
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (74) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (75) (1).png" alt=""><figcaption></figcaption></figure>

***

* I focused on port 445 which by default is used for the SMB protocol. I tried connecting using the [_sbmclient_](../../networks/tools-and-utilities.md#smbclient) tool to access the service to list the contents being shared. When asked for a password, I left it blank, and fortunately, I got the list of shares from the target machine

{% code lineNumbers="true" %}
```bash
smbclient -L 10.129.76.14 
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (76) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the SMB protocol you can go [here](../../networks/protocols/smb.md)
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (73) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: **4**

***

* After this, I tried accessing the shared folders and when doing it with the one named _WorkShares_, I gained access without being asked for a password

{% code lineNumbers="true" %}
```bash
smbclient //10.129.76.14/WorkShares
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (77) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (79) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**WorkShares**_

***

<figure><img src="../../.gitbook/assets/image (85) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**get**_

***

* Then I listed the content of the shared folder where I found some folders that seemed to belong to users of the target system. So I explored them, and when reaching the _James.P_ directory, I listed its content and found a _flag.txt_ file

<figure><img src="../../.gitbook/assets/image (80) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (81) (1).png" alt=""><figcaption></figcaption></figure>

***

* Knowing this, I used the internal `get` command to download the file from the SMB server and then I closed the connection. Finally, I checked the content of the file, retrieving from it the root flag

<figure><img src="../../.gitbook/assets/image (82) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (83) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (84) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**5f61c10dffbc77a704d76016a22f1664**_
