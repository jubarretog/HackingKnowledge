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

# Funnel (Tier 1)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark>**&#x20;1**
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> FTP / PostgreSQL / Reconnaissance / Tunneling / Password Spraying / Port Forwarding\
  &#x20;             / Anonymous-Guest Access / Clear Text Credentials

<figure><img src="../../.gitbook/assets/image (708).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.219.72 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (686).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the first question

<figure><img src="../../.gitbook/assets/image (407).png" alt=""><figcaption></figcaption></figure>

> Answer: _**2**_

***

* Then I did an exhaustive scan to learn more about the running services on the open ports

<pre class="language-basic" data-line-numbers><code class="lang-basic"><strong>nmap 10.129.219.72 -p21,22 -sVC -oN serv_scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (687).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* I identified two running services, focusing on the FTP protocol running on port 21, and tried logging in as an anonymous user and successfully got in

{% code overflow="wrap" lineNumbers="true" %}
```bash
ftp 10.129.219.72
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (688).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the FTP protocol you can go [here](../../networks/protocols/ftp.md)
{% endhint %}

***

* I checked the shared resources and found a folder named _mail\_backup._ I accessed it, listed its contents, and found two interesting files, which I downloaded from the server and closed the connection

<figure><img src="../../.gitbook/assets/image (689).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (408).png" alt=""><figcaption></figcaption></figure>

> Answer: _**mail\_backup**_

***

* I checked the contents of the downloaded files and found what seemed to be an email informing new employees of an enterprise about the password policy, and also a document containing the policy. Checking its content, I found valuable information letting me know that the default password used for the digital services was _funnel123#!#_

<figure><img src="../../.gitbook/assets/image (413).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (414).png" alt=""><figcaption><p>password_policy.pdf</p></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (692).png" alt=""><figcaption></figcaption></figure>

> Answer: _**funnel123#!#**_

***

* Now with this password, I could try to log in somewhere else. As I also found an SSH service running on the machine, I tried to log in there using one of the users exposed on the email. After trying with all the usernames I finally found that using _christine_ I successfully went in. After that, I sanitized the terminal to interact more comfortably with the system

{% code overflow="wrap" lineNumbers="true" %}
```bash
ssh christine@10.129.219.72
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (691).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (690).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn about the sanitization process you can go [here](../../linux/useful-shell-resources.md#tty-sanitization), and to learn more about the SSH protocol you can go [here](../../networks/protocols/ssh.md).
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (693).png" alt=""><figcaption></figcaption></figure>

> Answer: _**christine**_

***

* Then I wanted to find a way to escalate privileges. After exploring some escalation vectors I didn't find anything relevant, so to go deeper, I tried checking the programs running locally on the host. With this, I found a process running on port 5432

{% code overflow="wrap" lineNumbers="true" %}
```bash
ps aux | grep "127.0.0.1"
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (694).png" alt=""><figcaption></figcaption></figure>

***

* To get more details about it, I used the `ss` command to get information about the sockets running to relate any with the process found. I first listed the services showing the port the sockets were running on, and then the name of the service to relate them. With that, I confirmed that port 5432 was running the _postgresql program_

{% code overflow="wrap" lineNumbers="true" %}
```bash
ss -tuln
ss -tul
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (697).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions&#x20;

<figure><img src="../../.gitbook/assets/image (696).png" alt=""><figcaption></figcaption></figure>

> Answer: _**postgresql**_

***

<figure><img src="../../.gitbook/assets/image (698).png" alt=""><figcaption></figcaption></figure>

> Answer: _**local port forwarding**_

***

* As the service was locally deployed, I couldn't access or interact with it, but as I had access via _SSH_, I could try to make a tunnel via Local Port Forwarding so I could access it from my machine. So I mounted the tunnel through _SSH_ and after that, I checked in my machine that the service had been forwarded properly

{% code overflow="wrap" lineNumbers="true" %}
```bash
ssh -L 7777:127.0.0.1:5432 christine@10.129.219.72
ss -tlp
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (699).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (703).png" alt=""><figcaption></figcaption></figure>

***

* Then I could interact with the service to connect to the database. I tried using the [_Postgresql_](../../database-attacks/tools-and-utilities.md#postgresql) command line utility, specifying the location of the service in my machine and using the credentials I had got. Once I had done it, I connected successfully to the database

{% code overflow="wrap" lineNumbers="true" %}
```bash
psql -h 127.0.0.1 -p 7777 -U christine
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (704).png" alt=""><figcaption></figcaption></figure>

***

* Once there, I listed the databases and found an interesting one named _secrets_, so I accessed it and listed the tables finding a table named _flag_. Last, I retrieved all of the information from this table, and inside that, I found the flag

{% code overflow="wrap" lineNumbers="true" %}
```plsql
christine=# \l
christine=# \c secrets
secrets=# \dt
secrets=# SELECT * FROM flag;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (705).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the last questions

<figure><img src="../../.gitbook/assets/image (706).png" alt=""><figcaption></figcaption></figure>

> Answer: _**secrets**_

***

<figure><img src="../../.gitbook/assets/image (707).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Yes**_

***

* And finally, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**cf277664b1771217d7006acdea006db1**_
