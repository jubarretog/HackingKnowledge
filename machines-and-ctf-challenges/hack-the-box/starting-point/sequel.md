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

<figure><img src="../../../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>



## <mark style="color:blue;">Write-up</mark>

* We start doing an initial scan

{% code lineNumbers="true" %}
```bash
nmap -p- -Pn --min-rate 2000 10.129.122.150
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/image (179).png" alt=""><figcaption></figcaption></figure>

***

* With this we can answer the first question

<figure><img src="../../../.gitbook/assets/image (170).png" alt=""><figcaption></figcaption></figure>

> Answer: _**3306**_

***

* Now we make an exhaustive scan

{% code lineNumbers="true" %}
```bash
nmap -p3306 -sVC 10.129.122.150
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/image (178).png" alt=""><figcaption></figcaption></figure>

***

* With this and some research we can answer some questions

<figure><img src="../../../.gitbook/assets/image (171).png" alt=""><figcaption></figcaption></figure>

> Answer: _**MariaDB**_

***

<figure><img src="../../../.gitbook/assets/image (172).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-u**_

***

* To access the databasa we use the _mysql_ linux utility. As we don't know a username, we try inputing root as username and we gain access without being asked for password.

<figure><img src="../../../.gitbook/assets/image (180).png" alt=""><figcaption></figcaption></figure>

***

* With this and some research we can answer the next questions

<figure><img src="../../../.gitbook/assets/image (173).png" alt=""><figcaption></figcaption></figure>

> Answer: _**root**_

***

* With this we can answer the first question

<figure><img src="../../../.gitbook/assets/image (174).png" alt=""><figcaption></figcaption></figure>

> Answer: _**\***_

***

* With this we can answer the first question

<figure><img src="../../../.gitbook/assets/image (175).png" alt=""><figcaption></figcaption></figure>

> Answer: _**;**_

***

* Now we can enter SQL queries, so, we use `show databases;` command to enumerate the databases.

<figure><img src="../../../.gitbook/assets/image (181).png" alt=""><figcaption></figcaption></figure>

***

* With this we can answer the next question

<figure><img src="../../../.gitbook/assets/image (176).png" alt=""><figcaption></figcaption></figure>

> Answer: _**htb**_

***

* As we note, there is an unusual database called _htb_ then we access it using the SQL command `use htb;`

<figure><img src="../../../.gitbook/assets/image (182).png" alt=""><figcaption></figcaption></figure>

***

* Now we can list the tables in the database with `show tables;`

<figure><img src="../../../.gitbook/assets/image (183).png" alt=""><figcaption></figcaption></figure>

***

* If we read all information of table _config_ with `select * from config;`, we see there is a parameter called flag, so we can copy it an close the database.

<figure><img src="../../../.gitbook/assets/image (186).png" alt=""><figcaption></figcaption></figure>

***

* With this we have got the root flag and have pawned the machine

<figure><img src="../../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

> Answer: _**7b4bec00d1a39e3dd4e021ec3d915da8**_
