# Dog (Easy)

## <mark style="color:blue;">Description</mark>

* **Difficult** <mark style="color:green;">**->**</mark> Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **State** <mark style="color:green;">-></mark> Retired
* **Tags** <mark style="color:green;">-></mark> Pending

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/machines/651">https://app.hackthebox.com/machines/651</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap -p- -Pn --min-rate 2500 -oN scan.txt 10.129.16.169
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to learn more about the services running on the open ports

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -p22,80 -sVC -oN serv_scan.txt 10.129.16.169
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

***

* I found an HTTP service on port 80, so I tried accessing the content in the browser. I found a website, a blog about dogs, with some entries

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* Exploring the site, I reached de _About_ tab where we found information about the CMS that was being used by the page, and an email with a custom domain. Apart from that, I didn't get any other relevant information

<figure><img src="../../.gitbook/assets/image (921).png" alt=""><figcaption></figcaption></figure>

***

* So, I tried fuzzing the page to search for hidden directories or routes, and using the [_Gobuster_](../../web-exploitation/tools-and-utilities.md#gobuster) tool and a wordlist from [_SecLists_](../../web-exploitation/tools-and-utilities.md#daniel-miessler-wordlists), I found the _/.git_ route, which is related to a git repository and could give us information about the project and the source code&#x20;

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

***

* To help me explore the project, I used the [_Git-Dumper_](../../web-exploitation/tools-and-utilities.md#git-dumper) tool to fetch the files and reconstruct the repository locally. Once done, I started to check the files and reached the _settings.php_ file, where I found credentials for a database&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```bash
git clone https://github.com/arthaud/git-dumper
cd /git-dumper
pip install -r requirements.txt
python ~/Tools/git-dumper/git_dumper.py  http://10.129.16.169/.git/ ./repo
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

***

* I tried using them to log in to the website, but it didn't work. So, I keep searching for a valid username in the files, and by filtering data using the domain _dog.htb_ that we have found before, I fortunately found two email addresses. Once again, trying with the _tiffany_ user, I gained access to an administration panel

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

***

* I looked through the options to find any possible exploitation way, but didn't find anything relevant. So, I decided to search for possible known vulnerabilities for the version of the platform, and found a way to [exploit](https://www.exploit-db.com/exploits/52021) an RCE vulnerability in [_ExploitDB_](../../penetration-testing/process-stages/exploitation/tools-and-utilities.md#exploit-db). Reading the exploit found out that we could leverage a function to install modules, so I checked to confirm that option was present, and we fortunately found the upload point that would let us leverage the vulnerability

<figure><img src="../../.gitbook/assets/image (837).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (839).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (840).png" alt=""><figcaption></figcaption></figure>

***

* Then, I ran the exploit pointing to our target, which generated a compressed module that we could upload to the site. But first, I checked the created contents to ensure it had the correct payload, and noticed that we had to modify the _shell.php_ file to work properly for gaining a remote shell for us, as it was spawning _cmd,_ which wouldn't work correctly&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```bash
python exploit.py
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (841).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (842).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (843).png" alt=""><figcaption></figcaption></figure>

***

* So I edited it using a proper payload for the _Linux_ host and compressed the files again in a format that could be uploaded as a module. Then, I went to the upload point to submit the module, which worked without problems

{% code overflow="wrap" lineNumbers="true" %}
```bash
nano ./shell/shell.php
tar -cf shell.tar ./shell/shell.php ./shell/shell.info
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (844).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (845).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (838).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about how to craft and use a Reverse Shell properly, you can go [here](../../scripting/reverse-shell.md)
{% endhint %}

***

* With that done, I set a [_Netcat_](../../networks/tools-and-utilities.md#netcat) listener to receive the shell, and I went to the _/modules_ route, confirming the files were there. Then, I select the _shell.php_ file to trigger the script, noticing the listener had caught the shell. After that, I sanitized the terminal to work more comfortably

<figure><img src="../../.gitbook/assets/image (852).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (851).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (853).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (854).png" alt=""><figcaption></figcaption></figure>

***

* With that, I was able to go to the _/home_ folder to check for existing users, where I found two. Once there, I tried to log in as the _johncusack_ user using the same password we had found in the previous enumeration, which worked successfully, confirming a credential segregation vulnerability. With the new access, I was able to go to its home folder where there was a _user.txt_ file, and reading its content, I obtained the user flag

<figure><img src="../../.gitbook/assets/image (855).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (856).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the user flag

<figure><img src="../../.gitbook/assets/image (757).png" alt=""><figcaption></figcaption></figure>

> Answer: _**b63a7c1c6e4ba520e4a5d92cfde1b16c**_

***

* I tried looking for a way to escalate privileges, so first, I checked the privileged execution permissions for the user with `sudo -l` and I was able to execute the _/user/local/bin/bee_ binary. So, I checked the options that this binary had, finding that we have to specify the route to a Backdrop project, and one option that searched a file locally, and  the most relevant thing, an option that let us execute PHP code arbitrarily

<figure><img src="../../.gitbook/assets/image (850).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (847).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (848).png" alt=""><figcaption></figcaption></figure>

***

* So first, I searched for a Backdrop project on the whole system, finding it at the _/backdrop\_tool/bee/tests_ route. With that, I tried to run the binary specifying this folder and trying to run a system command, but it didn't work properly

<figure><img src="../../.gitbook/assets/image (849).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (846).png" alt=""><figcaption></figcaption></figure>

***

* It seemed not to be the actual root folder that was needed. So, thinking back that the web page used Backdrop, maybe we have to specify the root folder for the website project, which was on the _/var/www/ht&#x6D;_&#x6C; route. So I tried with that one, and executed a command to get a new shell, which this time worked properly and gave us a shell as the _root_ user

<figure><img src="../../.gitbook/assets/image (835).png" alt=""><figcaption></figcaption></figure>

***

* Finally, I navigated to the _/root_ folder where I found a _root.txt_ file, and reading its content, I obtained the root flag

<figure><img src="../../.gitbook/assets/image (836).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ea5d6ec20ff7c40598a7e1f95579455c**_
