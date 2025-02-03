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

# Sequel (Tier 1)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 1
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Vulnerability / Assessment / Databases / MySQL / SQL / Reconnaissance\
  &#x20;             / Weak Credentials

<figure><img src="../../.gitbook/assets/image (118) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap -p- -Pn --min-rate 2000 10.129.122.150
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (179) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the first question

<figure><img src="../../.gitbook/assets/image (170) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**3306**_

***

* Then I did an exhaustive scan to get information about the service running on the open port

{% code lineNumbers="true" %}
```bash
nmap -p3306 -sVC 10.129.122.150
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (178) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (171) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**MariaDB**_

***

<figure><img src="../../.gitbook/assets/image (172) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-u**_

***

* As we found the service running was a [_MariaDB_](https://mariadb.org/) database I used the [_mysql_](../../database-attacks/tools-and-utilities.md#mysql) Linux utility to connect to it. As I didn't have any credentials, I tried using _root_ as username and gained access without being asked for a password

{% code overflow="wrap" lineNumbers="true" %}
```bash
mysql -h 10.129.122.150 -u root
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (180) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (173) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**root**_

***

<figure><img src="../../.gitbook/assets/image (174) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**\***_

***

<figure><img src="../../.gitbook/assets/image (175) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**;**_

***

* With this, I could navigate through the database information using SQL queries. I enumerated the databases present noticing a particular one named _htb_ and accessed it

{% code overflow="wrap" lineNumbers="true" %}
```sql
show databases;
use htb;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (181) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (182) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about SQL you can go [here](../../database-attacks/sql.md)
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (176) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**htb**_

***

* Then I listed the tables in that database and found an interesting one named _config_. So I retrieved all the information from that table and saw there was a parameter called _flag_, which gave me the flag of the machine&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```sql
show tables;
select * from config;
exit
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (183) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (186) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (133) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**7b4bec00d1a39e3dd4e021ec3d915da8**_
