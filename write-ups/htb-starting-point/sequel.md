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

# Sequel

## <mark style="color:blue;">Description</mark>

* **Tier **<mark style="color:green;">**->**</mark> 1
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags **<mark style="color:green;">**->**</mark> Vulnerability / Assessment / Databases / MySQL / SQL / Reconnaissance\
  &#x20;             Weak Credentials

<figure><img src="../../.gitbook/assets/image (118).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* We start doing an initial scan

{% code lineNumbers="true" %}
```bash
nmap -p- -Pn --min-rate 2000 10.129.122.150
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (179).png" alt=""><figcaption></figcaption></figure>

***

* With this, we can answer the first question

<figure><img src="../../.gitbook/assets/image (170).png" alt=""><figcaption></figcaption></figure>

> Answer: _**3306**_

***

* Now we make an exhaustive scan

{% code lineNumbers="true" %}
```bash
nmap -p3306 -sVC 10.129.122.150
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (178).png" alt=""><figcaption></figcaption></figure>

***

* With this and some research, we can answer some questions

<figure><img src="../../.gitbook/assets/image (171).png" alt=""><figcaption></figcaption></figure>

> Answer: _**MariaDB**_

***

<figure><img src="../../.gitbook/assets/image (172).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-u**_

***

* To access the database we use the _mysql_ Linux utility. As we don't know a username, we try inputting _root_ as username and we gain access without being asked for a password

<figure><img src="../../.gitbook/assets/image (180).png" alt=""><figcaption></figcaption></figure>

***

* With this and some research, we can answer the next questions

<figure><img src="../../.gitbook/assets/image (173).png" alt=""><figcaption></figcaption></figure>

> Answer: _**root**_

***

* With this, we can answer the first question

<figure><img src="../../.gitbook/assets/image (174).png" alt=""><figcaption></figcaption></figure>

> Answer: _**\***_

***

* With this, we can answer the first question

<figure><img src="../../.gitbook/assets/image (175).png" alt=""><figcaption></figcaption></figure>

> Answer: _**;**_

***

* Now we can enter SQL queries. We use the `show databases;` command to enumerate the databases.

<figure><img src="../../.gitbook/assets/image (181).png" alt=""><figcaption></figcaption></figure>

***

* With this, we can answer the next question

<figure><img src="../../.gitbook/assets/image (176).png" alt=""><figcaption></figcaption></figure>

> Answer: _**htb**_

***

* As we note, there is an unusual database called _htb_. We access it using the `use htb;` command

<figure><img src="../../.gitbook/assets/image (182).png" alt=""><figcaption></figcaption></figure>

***

* Now we can list the tables in the database with the `show tables;` command

<figure><img src="../../.gitbook/assets/image (183).png" alt=""><figcaption></figcaption></figure>

***

* If we read all the information of the table _config_ with the `select * from config;` command, we see there is a parameter called _flag_, so we can copy it and close the database.

<figure><img src="../../.gitbook/assets/image (186).png" alt=""><figcaption></figcaption></figure>

***

* With this, we have got the root flag and have pawned the machine.

<figure><img src="../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

> Answer: _**7b4bec00d1a39e3dd4e021ec3d915da8**_
