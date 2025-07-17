# BountyHunter (Easy)

## <mark style="color:blue;">Description</mark>

* **Difficult** <mark style="color:green;">**->**</mark> Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **State** <mark style="color:green;">-></mark> Retired
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Vulnerability Assessment / Web Application / Source Code Analysis / XXE Injection\
  / Clear Text Credentials / Python

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/machines/359">https://app.hackthebox.com/machines/359</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap -p- -Pn --min-rate 2500 -oN scan.txt 10.129.95.166
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (811).png" alt=""><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to learn more about the services running on the open ports

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -p22,80 -sVC -oN serv_scan.txt 10.129.95.166
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (812).png" alt=""><figcaption></figcaption></figure>

***

* I found an HTTP service on port 80, so I tried accessing the content in the browser. There, I found a simple page for testing services, where some of the buttons didn't seem to work

<figure><img src="../../.gitbook/assets/image (813).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* Exploring the page and reading the source code, I didn't find anything relevant apart from a contact form, which didn't seem to do anything. Reaching the _Portal_ button in the top bar, redirected me to a page with a message that had a link to another page for testing purposes. This last one had a form for a reporting system that I filled and after hitting _Submit_, I noticed it showed me back the information given as a summary

<figure><img src="../../.gitbook/assets/image (868).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

***

* This made me think it could be vulnerable to an XSS vulnerability, but after some tests, it didn't go through. So I decided to look at the petition sent when filling out this form with the help of [_FoxyProxy_](../../web-exploitation/tools-and-utilities.md#foxyproxy) and [_Burp Suite_](../../web-exploitation/tools-and-utilities.md#burp-suite)_,_ and noticed it was sending a data parameter with an encoded value in the body. I used the decoder tab to decode this first from URL and then from Base64, seeing the content was an XML petition

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (816).png" alt=""><figcaption></figcaption></figure>

***

* Knowing this, I tried to test this for a possible XXE Injection, changing the content of the petition to add a payload to retrieve the content of the _/etc/passwd_ file and encoding it back into the initial format. Then I put this in the _data_ value and resent the petition, obtaining the desired result and confirming the vulnerability. Also, checking the content, I noticed there was a _development_ user in the system

<figure><img src="../../.gitbook/assets/image (817).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about XXE Injection, you can go [here](../../web-exploitation/broken-access-control/command-injection-1.md)
{% endhint %}

***

* As I knew this was an Apache server from my scan, I could search for possible PHP files on the system, but calling them directly would execute them instead of showing the source code. I investigated and found this could be bypassed by using PHP filters, so I did this by inserting a new payload to call the default _db.php_ file, re-did the encoding process, and sent it again, leaking the information from the database and some credentials&#x20;

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about bypassing using PHP filters, you can go [here](../../web-exploitation/broken-access-control/php-bypass-using-filters.md)
{% endhint %}

***

* With this, I tried assuming the _m19RoAU0hP41A1sTsq6K_ password found in this leak was the same to connect to the development user. So I used the SSH protocol to connect to the machine, and it worked, and after that, I sanitized the terminal to work more comfortably

{% code overflow="wrap" lineNumbers="true" %}
```bash
ssh development@10.129.95.166
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the SSH protocol, you can go [here](../../networks/protocols/ssh.md), and to learn more about the sanitization process, you can go [here](../../linux/useful-shell-resources.md#tty-sanitization)
{% endhint %}

***

* Once inside, I listed the contents of the folder where I was, which was the _/home_ folder of the user, finding a _user.txt_ file, and reading its content I retrieved the user flag



<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the user flag

<figure><img src="../../.gitbook/assets/image (757).png" alt=""><figcaption></figcaption></figure>

> Answer: _**bdc19bdcee275e01eef25a0c645b79db**_

***

* I needed to find a way to escalate privileges, but first, I looked at the content of the _contract.txt_ file, which was in the same location. The most relevant thing about the message was that the company had set permissions for the user to do testing on a tool. So I checked the privileged execution permissions with `sudo -l` and found the user could execute a _Python_ script as the root user

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

***

* I looked at the content of this script, which was a tool for handling tickets, and analyzed the flow of the actions. First, it asked the user to enter the path of the ticket, searched the file, and checked if it had the _.md_ extension to read its content. Then it checked that the first and second lines started with specific strings, and searched for a _Ticket Code_ section to make some validations about the ticket number and confirm if it was or not a valid ticket

<figure><img src="../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

***

* Also, in the folder where the script was, I found another folder with some examples for the construction of the tickets, which helped me understand better the format

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

***

* What caught my attention was that this script was using the _eval_ function, which is well-known for being vulnerable as it has global scope, and wasn't doing proper sanitization of the input. So I tried leveraging this, creating a ticket in the _/tmp_ folder based on the examples and internal validations, and adding a payload to spawn a shell in the part where the eval function would act. Then I ran the script using `sudo` and specifying the path to this ticket, which gave me a shell as the _root_ user

{% code overflow="wrap" lineNumbers="true" %}
```bash
nano shell.md
sudo /usr/bin/python3.8 /opt/skytrain_inc/ticketValidator.py
```
{% endcode %}

{% code title="shell.md" overflow="wrap" lineNumbers="true" %}
```markdown
# Skytrain Inc
## Ticket to New Haven
__Ticket Code:__
**11+9 == 20 and __import__('os').system('/bin/bash')**
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about abusing the _Python_ _eval_ function for privilege escalation, you can go [here](../../penetration-testing/process-stages/post-exploitation/privilege-escalation/linux-privilege-escalation.md#abusing-the-python-eval-function)
{% endhint %}

***

* Finally, I navigated to the _/root_ folder where I found a _root.txt_ file, and reading its content, I obtained the root flag

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**24f7090b6fd22d11acc7a2028eebe475**_
