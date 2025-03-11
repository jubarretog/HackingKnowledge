---
hidden: true
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

# Dog (Easy) (WIP)

## <mark style="color:blue;">Description</mark>

* **Difficult** <mark style="color:green;">**->**</mark> Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **State** <mark style="color:green;">-></mark> Retired
* **Tags** <mark style="color:green;">-></mark> Pending

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/machines/651">https://app.hackthebox.com/machines/651</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap -p- -Pn --min-rate 2500 -oN scan.txt 10.129.16.169
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to learn more about the services running on the open ports

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -p22,80 -sVC -oN serv_scan.txt 10.129.16.169
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

***

* I found an HTTP service on port 80 so I tried accessing the content on the browser. I

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol you can go [here](../../networks/protocols/http.md)
{% endhint %}

***

* E

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

***

* S

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

***

* A

{% code overflow="wrap" lineNumbers="true" %}
```bash
git clone https://github.com/arthaud/git-dumper
cd /git-dumper
pip install -r requirements.txt
python ~/Tools/git-dumper/git_dumper.py  http://10.129.16.169/.git/ ./repo
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

***

<figure><img src="../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

***

* d

<figure><img src="../../.gitbook/assets/image (837).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (839).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (840).png" alt=""><figcaption></figcaption></figure>

***

* s

```
python exploit.py
```

<figure><img src="../../.gitbook/assets/image (841).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (842).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (843).png" alt=""><figcaption></figcaption></figure>

***

* s

```
nano ./shell/shell.php
tar -cf shell.tar ./shell/shell.php ./shell/shell.info
```

<figure><img src="../../.gitbook/assets/image (844).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (845).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (838).png" alt=""><figcaption></figcaption></figure>

***

* dd

<figure><img src="../../.gitbook/assets/image (852).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (851).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (853).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (854).png" alt=""><figcaption></figcaption></figure>

***

*

<figure><img src="../../.gitbook/assets/image (855).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (856).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the user flag

<figure><img src="../../.gitbook/assets/image (757).png" alt=""><figcaption></figcaption></figure>

> Answer: _**d**_

***

* I tried looking for an

<figure><img src="../../.gitbook/assets/image (850).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (847).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (848).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (849).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (846).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (835).png" alt=""><figcaption></figcaption></figure>

***

* Finally, I navigated to the _/root_ folder where I found a _root.txt_ file, and reading its content I got the root flag

<figure><img src="../../.gitbook/assets/image (836).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**b6b99f7b44928603d26be1c7abae4d5c**_
