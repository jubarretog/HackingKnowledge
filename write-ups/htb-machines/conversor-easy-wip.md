---
hidden: true
---

# Conversor (Easy) (WIP)

## <mark style="color:blue;">Description</mark>

* **Difficult** <mark style="color:green;">**->**</mark> Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **State** <mark style="color:green;">-></mark> Active
* **Tags** <mark style="color:green;">-></mark> Pending



## <mark style="color:blue;">Write-up</mark>

* I started doing an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap -p- -Pn --min-rate 2500 -oN scan.txt 10.129.129.22
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (913).png" alt=""><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to learn more about the services running on the open ports

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -p22,80 -sVC -O -Pn -oN serv_scan.txt 10.129.129.22
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (914).png" alt=""><figcaption></figcaption></figure>

***

* I found an HTTP service on port 80, so I tried accessing the content in the browser. I found a website, a blog about dogs, with some entries

{% code overflow="wrap" lineNumbers="true" %}
```bash
echo "10.129.129.22 conversor.htb" | sudo tee -a /etc/hosts
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

sss

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* Exploring the site

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (915).png" alt=""><figcaption></figcaption></figure>

***

*

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (916).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (917).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (918).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (919).png" alt=""><figcaption></figcaption></figure>

***

* To h

{% code overflow="wrap" lineNumbers="true" %}
```bash
git
```
{% endcode %}



<figure><img src="../../.gitbook/assets/image (920).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (932).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (931).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (921).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (933).png" alt=""><figcaption></figcaption></figure>







***

* With that, I got the user flag

<figure><img src="../../.gitbook/assets/image (757).png" alt=""><figcaption></figcaption></figure>

> Answer: _**58da5b079ae088e2815663d343e22d8e**_

***

* I tried looki



***

* Finally, I navigated to the _/root_ folder where I found a _root.txt_ file, and reading its content, I obtained the root flag



***

* With that, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**e**_
