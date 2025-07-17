# Base (Tier 2)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 2
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Windows
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Vulnerability Assessment / Custom Applications / Source Code Analysis / Authentication\
  &#x20;              / Apache / PHP / Reconnaissance / Web Site Structure Discovery / SUDO Exploitation\
  &#x20;              / Authentication bypass / Clear Text Credentials / Arbitrary File Upload\
  &#x20;              / Information Disclosure / PHP type juggling

<figure><img src="../../.gitbook/assets/image (762).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=2</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.93.15 -p- -Pn --min-rate 2500 -oN scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (720).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the first question

<figure><img src="../../.gitbook/assets/image (721).png" alt=""><figcaption></figcaption></figure>

> Answer: _**22,80**_

***

* Then, to learn more about the services running on the open ports, I did an exhaustive scan

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>nmap 10.129.93.15 -p22,80 -sVC -oN serv_scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (732).png" alt=""><figcaption></figcaption></figure>

***

* I found the HTTP protocol running on port 80, so I went to the browser to explore the content and found a website for the services of a company. I explored the sections of the site, but for the moment, the only interesting thing was the _Contact_ section, which had a form that I filled out, but when I tried to submit, it didn't work and showed an error message

<figure><img src="../../.gitbook/assets/image (726).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (725).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* I continued exploring the sections, reaching the _Login_ button, which redirected me to a login page. I tried logging in with common credentials, but it didn't work. What caught my attention was the route to this site on the URL, which wasn't calling the source file directly but using a relative route. Based on this, I tried reaching just the folder from which it was being taken and noticed other exposed files

<figure><img src="../../.gitbook/assets/image (728).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (729).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, we answered the next questions

<figure><img src="../../.gitbook/assets/image (727).png" alt=""><figcaption></figcaption></figure>

> Answer: _**/login/login.php**_

***

<figure><img src="../../.gitbook/assets/image (730).png" alt=""><figcaption></figcaption></figure>

> Answer: _**3**_

***

<figure><img src="../../.gitbook/assets/image (731).png" alt=""><figcaption></figcaption></figure>

> Answer: _**.swp**_&#x73;trcmp()

***

* With a little research, I found that the _.swp_ extension is for temporary files from text editors such as _vi, vim, nvim_, etc, so I downloaded the _login.php.swp_ file and used the `vim` command with the `-r` flag to recover the file, save it to a new file, and read its content, now visualizing the source code properly. We noticed it was making a comparison for the confirmation of the credentials using the _strcmp_ function

{% code overflow="wrap" lineNumbers="true" %}
```bash
vim -r login.php.swp 

# Inside vim
:w login.php
:q!
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (733).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (734).png" alt=""><figcaption></figcaption></figure>

> Answer: _**strcmp()**_

***

* So, searching about this function and its possible flaws, I found out that it could be affected via _PHP_ Type Juggling, by passing the parameters from the request as arrays instead of variables. So I intercepted the petition to modify it using [_FoxyProxy_](../../web-exploitation/tools-and-utilities.md#foxyproxy) and [_Burp Suite_](../../web-exploitation/tools-and-utilities.md#burp-suite), then forwarded it, and reached a new page with an upload option

<figure><img src="../../.gitbook/assets/image (735).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (738).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (739).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about _PHP_ Type Juggling, you can go [here](../../web-exploitation/broken-access-control/php-abuse-php-type-juggling.md)
{% endhint %}

***

* Once here, I tried uploading a script for getting a reverse shell in _PHP_, and it worked, but I didn't know where the files were being saved. So, to find the location, I tried fuzzing the URL to find possible routes, and after some attempts and finding the correct dictionary, I found a route _/\_uploaded,_ which seemed to be the correct location. Then I went to that route and confirmed the file was there

{% code overflow="wrap" lineNumbers="true" %}
```bash
gobuster dir -u http://10.129.93.15 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt -o fuzz.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (761).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (740).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (743).png" alt=""><figcaption></figcaption></figure>

> Answer: _**/\_uploaded**_

***

* So, to gain the reverse shell, I set up a [_Netcat_](../../networks/tools-and-utilities.md#netcat) listener to catch the connection and tried accessing the file from the browser. I noticed it kept loading, and the listener successfully caught the connection. Then, I sanitized the terminal to interact better with it

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nvlp 4444
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (745).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (741).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (742).png" alt=""><figcaption></figcaption></figure>

***

* As I was a default user from the web server, I had to find a way to make lateral movement to another user on the system with less restricted actions. First, I went to explore the server files in the default folder _/var/www/html,_ finding a curious file under the _/login_ folder named _config.php_, and checking its content, I found a password for the _admin_ user was being leaked

<figure><img src="../../.gitbook/assets/image (747).png" alt=""><figcaption></figcaption></figure>

***

* I had the credentials for a user on the website, but I was looking for one on the system, so maybe these credentials could also work there. I tried changing to the user _admin,_ but it failed, so it wasn't a user on the system. So I went to the _/home_ folder to see if there was any folder related to another user and found one named _john_. Once again, I tried changing to that user, assuming it would have the same password, and it worked successfully

<figure><img src="../../.gitbook/assets/image (748).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next questions

<figure><img src="../../.gitbook/assets/image (751).png" alt=""><figcaption></figcaption></figure>

> Answer: _**john**_

***

<figure><img src="../../.gitbook/assets/image (752).png" alt=""><figcaption></figcaption></figure>

> Answer: _**thisisagoodpassword**_

***

* Once there, I went to its _/home_ folder, found a _user.txt_ file, and retrieved the user flag from its content



<figure><img src="../../.gitbook/assets/image (749).png" alt=""><figcaption></figcaption></figure>

***

* What was left was to escalate privileges, so I checked the `sudo` execution permissions for this user, and it could execute the `find` command as a privileged user

<figure><img src="../../.gitbook/assets/image (753).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next questions

<figure><img src="../../.gitbook/assets/image (754).png" alt=""><figcaption></figcaption></figure>

> Answer: _**/usr/bin/find**_

***

<figure><img src="../../.gitbook/assets/image (756).png" alt=""><figcaption></figcaption></figure>

> Answer: _**exec**_

***

<figure><img src="../../.gitbook/assets/image (757).png" alt=""><figcaption></figcaption></figure>

> Answer: _**f54846c258f3b4612f78a819573d158e**_

***

* Knowing that, I went to [_GTFOBins_](../../penetration-testing/process-stages/post-exploitation/tools-and-utilities.md#gtfobins) to see if there was any related exploitation for the `sudo` permissions on this binary, and fortunately, it was, so I used it and successfully gained a shell as the _root_ user

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo find . -exec /bin/sh \; -quit
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (758).png" alt=""><figcaption></figcaption></figure>

***

* Finally, I went to the _/root_ folder and listed its content, noticing a _root.txt_ file, and reading its contents, I obtained the root flag

<figure><img src="../../.gitbook/assets/image (759).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**51709519ea18ab37dd6fc58096bea949**_
