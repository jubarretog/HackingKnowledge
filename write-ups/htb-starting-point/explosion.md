# Explosion (Tier 0)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 0
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Windows
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Programming / RDP / Reconnaissance / Weak Credentials

<figure><img src="../../.gitbook/assets/image (34) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=0">https://app.hackthebox.com/starting-point?tier=0</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* With a little research, I started answering the first questions

<figure><img src="../../.gitbook/assets/image (20) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Remote Desktop Protocol**_

***

<figure><img src="../../.gitbook/assets/image (21) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**cli**_

***



<figure><img src="../../.gitbook/assets/image (22) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**gui**_

***

<figure><img src="../../.gitbook/assets/image (23) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**telnet**_

***

<figure><img src="../../.gitbook/assets/image (31) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**nmap**_

***

* Then I continued doing an initial port scan of the machine using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.1.13 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (25) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (24) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ms-wbt-server**_

***

<figure><img src="../../.gitbook/assets/image (26) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**/v:**_

***

* Then I did an exhaustive scan of the ports found to get information about the running services

{% code lineNumbers="true" %}
```bash
nmap 10.129.1.13 -p135,139,445,3389,5985,47001 -sVC -oN serv_scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (28) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (29) (1).png" alt=""><figcaption></figcaption></figure>

***

* I observed the RDP protocol was running on port 3389, so I tried to access it using the [_xfreerdp_](../../networks/tools-and-utilities.md#xfreerdp) tool. But as I was only able to provide the IP, it asked for a domain and password, which I didn't have. So I tried to log in using common credentials, and when using _administrator_ as username, I could log in providing a blank password, gaining remote access to the machine as a privileged user

{% code overflow="wrap" lineNumbers="true" %}
```bash
xfreerdp /v:10.129.1.13
xfreerdp /v:10.129.1.13 /u:administrator
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (30) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (31) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (32) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the RDP protocol, you can go [here](../../networks/protocols/rdp.md)
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (27) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**administrator**_

***

* Once inside, I saw on the Desktop there was a file named _flag,_ which seemed to be a text file, so I opened it to look at its content, and with this, I retrieved the root flag

<figure><img src="../../.gitbook/assets/image (33) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (39) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**951fa96d7830c451b536be5a6be008a0**_
