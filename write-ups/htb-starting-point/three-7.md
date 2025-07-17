# Oopsie (Tier 2)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 2
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> PHP / Custom Applications / Apache / Reconnaissance / Web Site Structure Discovery\
  &#x20;              / Cookie Manipulation / SUID Exploitation / Authentication Bypass / Clear Text Credentials\
  &#x20;              / Arbitrary File Upload / Insecure Direct Object Reference (IDOR) / Path Hijacking

<figure><img src="../../.gitbook/assets/image (763).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=2</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* With a little research, I started answering the first question

<figure><img src="../../.gitbook/assets/image (524).png" alt=""><figcaption></figcaption></figure>

> Answer: &#x50;_**roxy**_

***

* Then I did an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.123.87 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (264).png" alt=""><figcaption></figcaption></figure>

***

* After that, I also did an exhaustive scan to know about the services running on the open ports

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.123.87 -p22,80 -sVC -oN serv_scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (265).png" alt=""><figcaption></figcaption></figure>

***

* I found an HTTP service running on port 80, which meant a web page was being deployed. So, I went and checked it on the browser and found a simple page where none of the buttons seemed to work. The only relevant thing I saw was an email at the bottom of the site

<figure><img src="../../.gitbook/assets/image (266).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (268).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* So, to get more information, I tried to find some possible directories and files exposed on the web through _fuzzing_. To help me with that, I used [_Gobuster_](../../web-exploitation/tools-and-utilities.md#gobuster) and a common dictionary from [_SecLists_](../../web-exploitation/tools-and-utilities.md#daniel-miessler-wordlists). But even trying various dictionaries, I didn't find anything relevant apart from some basic server routes for which I didn't have access permissions

{% code overflow="wrap" lineNumbers="true" %}
```bash
gobuster dir -u http://10.129.123.87 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -o fuzz.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (275).png" alt=""><figcaption></figcaption></figure>

***

* So I reviewed the source code of the website, and in the final part, I found a script tag that was calling a _JavaScript_ file from another URL that seemed to be a login. With this, I tried navigating to that route, and fortunately, I found a login page

<figure><img src="../../.gitbook/assets/image (532).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (269).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (536).png" alt=""><figcaption></figcaption></figure>

> Answer: _**/cdn-cgi/login**_

***

* I tried to log in with common credentials, but it didn't work. Also, I saw there was an option for logging in as a guest, so I used it and went to an administration page. Exploring the tabs, what I found the most relevant was the _Uploads_ tab, where maybe I could abuse a File Upload vulnerability, but the page asked us for admin permissions&#x20;

<figure><img src="../../.gitbook/assets/image (270).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (271).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about File Upload and its exploitation, you can go [here](../../web-exploitation/broken-access-control/abuse-file-upload.md)
{% endhint %}

***

* I continued checking the _Account_ tab, where I saw what seemed to be information about the current user, including that the site assigned an _Access ID_ to every user. Also, I noticed that in the URL, a parameter _id_ was being queried to display the page, but it wasn't the same _Access ID_. So I tried to modify it, setting its value to 1, and I found this section was vulnerable to IDOR, revealing information about the _admin_ user

<figure><img src="../../.gitbook/assets/image (272).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (274).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the Insecure Direct Object Reference (IDOR) vulnerability and its exploitation, you can go [here](../../web-exploitation/owasp-top-10/broken-access-control.md)
{% endhint %}

***

* With this, I had more information to find a way to access the _Uploads_ section. So to check how it was working, I tried intercepting the petition with [_FoxyProxy_](../../web-exploitation/tools-and-utilities.md) and sending it to [_Burp Suite_](../../web-exploitation/tools-and-utilities.md#burp-suite) to analyze it and replicate it

<figure><img src="../../.gitbook/assets/image (276).png" alt=""><figcaption></figcaption></figure>

***

* I saw a _Cookie_ header was being sent in the petition with the parameters _user_ and _role_, noticing the value of _user_ was the _Account ID_ I could see in the _Account_ section. I tried modifying this value with the one leaked for the _admin_ user and then forwarding the petition, and it gave me access to the _Uploads_ panel with administration permissions, impersonating the user

<figure><img src="../../.gitbook/assets/image (278).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (279).png" alt=""><figcaption></figcaption></figure>

***

* With this information, I answered the next questions

<figure><img src="../../.gitbook/assets/image (223).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Cookie**_

***

<figure><img src="../../.gitbook/assets/image (225).png" alt=""><figcaption></figcaption></figure>

> Answer: _**34322**_

***

* To abuse this functionality, and knowing that the page was made in [_PHP_](https://www.php.net/) thanks to [_Wappalyzer_](../../web-exploitation/tools-and-utilities.md#wappalyzer), I tried uploading a Reverse Shell for _PHP_. At the moment of sending the petition, I modified again the _user_ parameter to retain the privileges, and saw that the process worked, and the file was uploaded

<figure><img src="../../.gitbook/assets/image (280).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (281).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (282).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (283).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about how to create a script for a Reverse Shell, you can go [here](../../scripting/reverse-shell.md)
{% endhint %}

***

* I needed to find a form to invoke our file in the system, but didn't know exactly where the file was. So, going back to the fuzzing results, there was a _/uploads_ route, which is a default route for uploaded files in _PHP_. So assuming here would be the file, I set up a [_Netcat_](../../networks/tools-and-utilities.md#netcat) listener and went to this route calling the file, and fortunately, I caught a shell from the target machine as the _www-data_ user. Also, I sanitized the terminal to work more comfortably with it

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nvlp 4444
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (284).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (285).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (246).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn about the sanitization process, you can go [here](../../linux/useful-shell-resources.md#tty-sanitization)
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (248).png" alt=""><figcaption></figcaption></figure>

> Answer: _**/uploads**_

***

* Then, I had to find a way to make lateral movement to another user, as _www-data_ is the default for some web servers and usually doesn't have permission for some actions. I explored the filesystem starting with the _/var/www/html_ route, where the information of the web server is usually found. There, I found in the _cdn-cgi/login_ folder, there was a _db.php_ file that seemed to be database information, and reading its content, we found some exposed credentials for the user _robert_

<figure><img src="../../.gitbook/assets/image (286).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (252).png" alt=""><figcaption></figcaption></figure>

> Answer: _**db.php**_

***

* With this information, I tried changing to the user _robert_ and it worked successfully, being able to navigate to the home folder of this user, where I found a _user.txt_ file, and reading its content, I retrieved the user flag

<figure><img src="../../.gitbook/assets/image (287).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (288).png" alt=""><figcaption></figcaption></figure>

***

* What was left was to find a way to escalate privileges. I started looking at the execution permissions for the `sudo` command, but nothing was enabled. Then, I searched for executables with SUID permissions that we could abuse, and found that there was a binary named _bugtracker_ with special permissions as the _root_ user, and for the members of the _bugtracker_ group. I checked and fortunately, our user was in this group, so I could abuse it

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo -l
find / -type f -perm -04000 -ls 2>/dev/null | grep bin
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (253).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (256).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (255).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (260).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more the abuse of SUID/SGID for privilege escalation, you can go [here](../../penetration-testing/process-stages/post-exploitation/privilege-escalation/#abusing-suid-sgid-permissions-on-reading-binaries)
{% endhint %}

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (254).png" alt=""><figcaption></figcaption></figure>

> Answer: _**find**_

***

<figure><img src="../../.gitbook/assets/image (258).png" alt=""><figcaption></figcaption></figure>

> Answer: _**root**_

***

<figure><img src="../../.gitbook/assets/image (259).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Set Owner User ID**_

***

* So I tried running the binary to see how it worked. It displayed a report of bugs based on a provided _ID_ value, but when given an arbitrary number whose report was not in the system, it gave us an error where the content of a file couldn't be found and displayed, apparently using the `cat` command

<figure><img src="../../.gitbook/assets/image (261).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (263).png" alt=""><figcaption></figcaption></figure>

***

* Also, I noticed it seemed to be using the relative route for calling the `cat` binary instead of the absolute route, and that could make it vulnerable to a Path Hijacking attack. So to confirm, I used the command `strings` on the binary hoping to get some information about the code with which it was built, and in fact, I saw it was calling it relatively

{% code overflow="wrap" lineNumbers="true" %}
```bash
strings /usr/bin/bugtracker
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (295).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* With this and the previously found user flag, I answered the next questions

<figure><img src="../../.gitbook/assets/image (296).png" alt=""><figcaption></figcaption></figure>

> Answer: _**cat**_

***

<figure><img src="../../.gitbook/assets/image (297).png" alt=""><figcaption></figcaption></figure>

> Answer: _**f2c74ee8db7983851ab2a96a44eb7981**_

***

* So I tried performing this attack by adding the /_home/robert_ route to the _PATH_ environment variable and creating an arbitrary version of the `cat` binary to invoke a shell with privileges. Then I executed again the _bugtracker_ binary, which would call my version of the binary, noticing it worked, and getting a shell as the _root_ user

<figure><img src="../../.gitbook/assets/image (292).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (293).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about Path Hijacking exploitation, you can go [here](../../penetration-testing/process-stages/post-exploitation/privilege-escalation/linux-privilege-escalation.md#abusing-the-path-environment-variable-path-hijacking)
{% endhint %}

***

* Finally, I went to the _/root_ folder to look at its content, noticing a _root.txt_ file. Before reading it, I rolled back the _PATH_ variable to its default to ensure the `cat` command would work normally again, and with this, I finally retrieved the root flag&#x20;

<figure><img src="../../.gitbook/assets/image (294).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**af13b0bee69f8a877c3faf667f7beacf**_
