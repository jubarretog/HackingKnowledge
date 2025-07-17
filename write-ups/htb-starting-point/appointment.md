# Appointment (Tier 1)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 1
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Databases / Apache / MariaDB / PHP / SQL / Reconnaissance / SQL Injection

<figure><img src="../../.gitbook/assets/image (117) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* With some research, I started answering the first questions

<figure><img src="../../.gitbook/assets/image (122) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Structured Query Language**_

***

<figure><img src="../../.gitbook/assets/image (124) (1).png" alt=""><figcaption></figcaption></figure>

> Anwer: _**SQL Injection**_

***

<figure><img src="../../.gitbook/assets/image (125) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**A03:2021 Injection**_

***

* Then, I did an initial scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p- -Pn --min-rate 2000 10.129.228.241
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (134) (1).png" alt=""><figcaption></figcaption></figure>

***

* I continued doing an exhaustive scan on the open port to know about the services running

{% code lineNumbers="true" %}
```bash
nmap -p80 -sVC 10.129.228.241
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (135) (1).png" alt=""><figcaption></figcaption></figure>

***

* With that and some research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (126) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Apache httpd 2.4.38 ((Debian))**_

***

<figure><img src="../../.gitbook/assets/image (128) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**443**_

***

<figure><img src="../../.gitbook/assets/image (127) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Directory**_

***

<figure><img src="../../.gitbook/assets/image (129) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**404**_

***

<figure><img src="../../.gitbook/assets/image (130) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**dir**_

***

<figure><img src="../../.gitbook/assets/image (131) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**#**_

***

* As I found an HTTP service running on port 80, I went to the browser to explore the content being deployed. I found a simple login page and tried to log in with some default credentials, but it didn't work

<figure><img src="../../.gitbook/assets/image (136) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* So, looking for another way to get through this, I tried doing some basic _SQL Injection_ tests, assuming that was the way the credentials were being validated.  After some tries, I found out that by using the username _admin'#_ and providing any password (a basic test for _SQLi_ in PHP-based pages), I gained access, and a message with the flag was displayed

<figure><img src="../../.gitbook/assets/image (137) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about Authentication bypass via SQLi, you can go [here](../../database-attacks/specific-scenarios/sql-injection/authentication-bypass.md)
{% endhint %}

***

* With this, I answered the last question

<figure><img src="../../.gitbook/assets/image (132) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Congratulations**_

***

* And finally, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (133) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**e3d0796d002a446c0e622226f42e9672**_
