# Ignition (Tier 1)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark>**&#x20;1**
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Common Applications / Magento / Reconnaissance / Web Site Structure Discovery\
  &#x20;             / Weak Credentials

<figure><img src="../../.gitbook/assets/image (685).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.246.174 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (665).png" alt=""><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to learn more about the services running on the open ports

{% code lineNumbers="true" %}
```bash
nmap 10.129.246.174 -p80 -sVC -oN serv_scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (666).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the first question

<figure><img src="../../.gitbook/assets/image (667).png" alt=""><figcaption></figcaption></figure>

> Answer: _**nginx 1.14.2**_

***

* As I found the HTTP protocol running on port 80, I visited the deployed content in the browser. When I tried to reach the site using the IP address, it redirected me to the _ignition.htb_ domain whose content wasn't possible to display

<figure><img src="../../.gitbook/assets/image (670).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* To check what could be happenin,g I used the `curl` command to get information from the response of the petition sent to the web. This could be because I didn't have the domain in our list of known hosts. So to solve that, I added it to the _/etc/hosts and &#x61;_&#x66;ter that visited the site again and it worked properly

{% code overflow="wrap" lineNumbers="true" %}
```bash
curl -v http://10.129.246.174
echo '10.129.246.174 ignition.htb' >> /etc/hosts
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (675).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (671).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (676).png" alt=""><figcaption></figcaption></figure>

> Answer: _**302**_

***

<figure><img src="../../.gitbook/assets/image (677).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ignition.htb**_

***

<figure><img src="../../.gitbook/assets/image (678).png" alt=""><figcaption></figcaption></figure>

> Answer: _**/etc/hosts**_

***

* I explored the features of the page but didn't find anything relevant, so I tried fuzzing the URL using [_Gobuster_](../../web-exploitation/tools-and-utilities.md#gobuster) to find some possible directories and files exposed on the web

{% code overflow="wrap" lineNumbers="true" %}
```bash
gobuster dir -u http://ignition.htb -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -o fuzz.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (681).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* I found some interesting routes, the most relevant being the _/admin_ route, so I navigated there to see the content and found a login page for the [_Magento_](https://business.adobe.com/co/products/magento/magento-commerce.html) CMS

<figure><img src="../../.gitbook/assets/image (679).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (680).png" alt=""><figcaption></figcaption></figure>

> Answer: _**http://ignition.htb/admin**_

***

<figure><img src="../../.gitbook/assets/image (682).png" alt=""><figcaption></figcaption></figure>

> Answer:&#x20;

***

* As I didn't have any credentials, I tried using some common credentials, and doing a little [research](https://community.spiceworks.com/t/most-common-passwords-of-2023-the-top-10/963430) about this topic, I found that by using the username _admin_ and the password _qwerty123_ I gained access to the administrator dashboard. Finally, looking at the deployed content, I found the flag at first sight

<figure><img src="../../.gitbook/assets/image (683).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**797d6c988d9dc5865e010b9410f247e0**_
