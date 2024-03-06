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

# Crocodile

## <mark style="color:blue;">Description</mark>

* **Tier **<mark style="color:green;">**->**</mark> 1
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags **<mark style="color:green;">**->**</mark> Custom Applications / Protocols / Apache / FTP / Reconnaissance\
  &#x20;             Web Site Structure Discovery / Clear Text Credentials / Anonymous-Guest Access

<figure><img src="../../../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>



## <mark style="color:blue;">Write-up</mark>

* We start answering the first question with some research

<figure><img src="../../../.gitbook/assets/image (196).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-sC**_

***

* After this, we make an initial scan

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p- -Pn --min-rate 2000 10.129.1.15
</strong></code></pre>

<figure><img src="../../../.gitbook/assets/image (198).png" alt=""><figcaption></figcaption></figure>

***

* Now we can make exhaustive scan

{% code lineNumbers="true" %}
```bash
nmap -p21,80 -sVC 10.129.1.15
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/image (199).png" alt=""><figcaption></figcaption></figure>

***

* With this we answer the next question

<figure><img src="../../../.gitbook/assets/image (197).png" alt=""><figcaption></figcaption></figure>

> Answer: _**vsftpd 3.0.3**_

***

* Now we use _ftp_ on command line to connect to the machine with the protocol. We access with _anonymous_ user as our previous scan reported us it was posible.

<figure><img src="../../../.gitbook/assets/image (200).png" alt=""><figcaption></figcaption></figure>

***

* Now we can answer some questions

<figure><img src="../../../.gitbook/assets/image (209).png" alt=""><figcaption></figcaption></figure>

> Answer: _**230**_

***

<figure><img src="../../../.gitbook/assets/image (210).png" alt=""><figcaption></figcaption></figure>

> Answer: _**anonymous**_

***

<figure><img src="../../../.gitbook/assets/image (211).png" alt=""><figcaption></figcaption></figure>

> Answer: _**get**_

***

* Once we have acessed we list the contents with `ls` and find 2 files that seems to be user's data

<figure><img src="../../../.gitbook/assets/image (191).png" alt=""><figcaption></figcaption></figure>

***

* We use `mget *` to download both of the files and then close the connection

<figure><img src="../../../.gitbook/assets/image (193).png" alt=""><figcaption></figcaption></figure>

***

* Now we check the content of both files and we found what seems to be a list of usernames and a list of related passwords.&#x20;

<figure><img src="../../../.gitbook/assets/image (194).png" alt=""><figcaption></figcaption></figure>

***

* With this, some reasearch and previous information got on the scans, we can answer some questions

<figure><img src="../../../.gitbook/assets/image (212).png" alt=""><figcaption></figcaption></figure>

> Answer: _**admin**_

***

<figure><img src="../../../.gitbook/assets/image (213).png" alt=""><figcaption></figcaption></figure>

> Answer: _**apache httpd 2.4.41**_

***

<figure><img src="../../../.gitbook/assets/image (214).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-x**_

***

* With this information we can check if credentials work on the ftp service. But if we try with any of the usernames it will notify us that it only allows anonymous connection.

<figure><img src="../../../.gitbook/assets/image (201).png" alt=""><figcaption></figcaption></figure>

***

* &#x20;Now what's left is to check out the other running service. It is a http on port 80, which meens is a web page. We can check it on a browser.

<figure><img src="../../../.gitbook/assets/image (202).png" alt=""><figcaption></figcaption></figure>

***

* As we explore explore trough the sections of the page we will notice that it does not redirect us to any other page, and the unic different thing is a form in the contact section but seems it does not work properly.

<figure><img src="../../../.gitbook/assets/image (203).png" alt=""><figcaption></figcaption></figure>

***

* Also the Wappalyzer extension give us some inofrmation about the page technologies

<figure><img src="../../../.gitbook/assets/image (205).png" alt=""><figcaption></figcaption></figure>

***

* As we did not find anything interesting on first instance, we could try to fuzz the page using _gobuster_ and a dictionary. Also as we know the page is written on php as found above, we can specify it on the fuzzing.

{% code overflow="wrap" lineNumbers="true" %}
```bash
gobuster dir -u -w http://10.129.1.15/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/image (206).png" alt=""><figcaption></figcaption></figure>

***

* &#x20;As the fuzz goes on we find some interesting directions, being the most striking one _login.php_. We go to the new direction and we find a login page.

<figure><img src="../../../.gitbook/assets/image (208).png" alt=""><figcaption></figcaption></figure>

***

* With this we can answer another question

<figure><img src="../../../.gitbook/assets/image (215).png" alt=""><figcaption></figcaption></figure>

> Answer: _**login.php**_

***

* If we try with the credentials found in the lists previously, combining the usernames with the passwords, we find that with username _root_ and password _rKXM59ESxesUFHAd_ we get acces to the administration panel of the web page and a message is displayed.

<figure><img src="../../../.gitbook/assets/image (207).png" alt=""><figcaption></figcaption></figure>

***

* With this we have got the root flag and have pawned the machine

<figure><img src="../../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

> Answer: _**c7110277ac44d78b6a9fff2232434d16**_
