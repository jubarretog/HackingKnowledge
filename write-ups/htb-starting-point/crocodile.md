# Crocodile (Tier 1)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 1
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Custom Applications / Protocols / Apache / FTP / Reconnaissance\
  &#x20;            / Web Site Structure Discovery / Clear Text Credentials / Anonymous-Guest Access

<figure><img src="../../.gitbook/assets/image (119) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* With some research, I started answering the first question&#x20;

<figure><img src="../../.gitbook/assets/image (196) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-sC**_

***

* After this, I did an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p- -Pn --min-rate 2000 10.129.1.15
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (198) (1).png" alt=""><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to get information about the services running on the open ports

{% code lineNumbers="true" %}
```bash
nmap -p21,80 -sVC 10.129.1.15
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (199) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (197) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**vsftpd 3.0.3**_

***

* I found the FTP protocol running on its default port, so I tried connecting to it. As I didn't have any credentials, I tried using the _anonymous_ user and it let me in successfully

<figure><img src="../../.gitbook/assets/image (200) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the FTP protocol, you can go [here](../../networks/protocols/ftp.md)
{% endhint %}

***

* With that and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (209) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**230**_

***

<figure><img src="../../.gitbook/assets/image (210) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**anonymous**_

***

<figure><img src="../../.gitbook/assets/image (211) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**get**_

***

* Once I had access, I listed the contents being shared on the server and found 2 files that seemed to be users' data. So I downloaded both of the files and then closed the connection

{% code overflow="wrap" lineNumbers="true" %}
```bash
ls
mget *
exit
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (191) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (193) (1).png" alt=""><figcaption></figcaption></figure>

***

* I checked the content of both files and found what seemed to be a list of usernames and a list of related passwords

{% code overflow="wrap" lineNumbers="true" %}
```bash
cat allowed.userlist allowed.userlist.passwd
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (194) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, a little research, and the previous information obtained from the scans, I answered the next questions

<figure><img src="../../.gitbook/assets/image (212) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**admin**_

***

<figure><img src="../../.gitbook/assets/image (213) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**apache httpd 2.4.41**_

***

<figure><img src="../../.gitbook/assets/image (214) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-x**_

***

* With this information, I could check if these credentials work on the FTP service. But after trying all the usernames, it notified me that it only allows anonymous connections

<figure><img src="../../.gitbook/assets/image (201) (1).png" alt=""><figcaption></figcaption></figure>

***

* So I decided to check the other running service. It was an HTTP on port 80, so I went to the browser to look at the content being deployed. I found a dashboard for the services of a company where any of the buttons seemed to work

<figure><img src="../../.gitbook/assets/image (202) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* After exploring the sections of the page, the unique interesting thing was a form in the contact section, which didn't seem to be working properly. To get some extra information about the components of the website, I used the [_Wappalyzer_](../../web-exploitation/tools-and-utilities.md#wappalyzer) extension, but it didn't give me anything relevant

<figure><img src="../../.gitbook/assets/image (203) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (205) (1).png" alt=""><figcaption></figcaption></figure>

***

* As I didn't find anything interesting in the first instance, I tried to fuzz the page using [_Gobuster_](../../web-exploitation/tools-and-utilities.md#gobuster) and a dictionary. Also, as I knew the page was written on _PHP,_ thanks to _Wappalyzer_, I specified this on the fuzzing options

{% code overflow="wrap" lineNumbers="true" %}
```bash
gobuster dir -u -w http://10.129.1.15/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -x php,html
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (206) (1).png" alt=""><figcaption></figcaption></figure>

***

* &#x20;The fuzzing gave me some interesting directions, giving my attention to the _/login.php_ route, so I visited this direction and found a simple login page

<figure><img src="../../.gitbook/assets/image (208) (1).png" alt=""><figcaption></figcaption></figure>

***

* With that, I answered the next question

<figure><img src="../../.gitbook/assets/image (215) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**login.php**_

***

* Once there, I tried using again the credentials found in the previous lists, combining the usernames with the passwords, and by using the username _root_ and the password _rKXM59ESxesUFHAd,_ I gained access to an administration panel where a message with the flag was displayed

<figure><img src="../../.gitbook/assets/image (207) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (133) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**c7110277ac44d78b6a9fff2232434d16**_
