# Mongod (Tier 0)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 0
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> MongoDB / Databases / Reconnaissance Misconfiguration / Anonymous-Guest Access

<figure><img src="../../.gitbook/assets/image (57) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=0">https://app.hackthebox.com/starting-point?tier=0</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial port scan of the machine using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.1.138 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (53) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the first question

<figure><img src="../../.gitbook/assets/image (593).png" alt=""><figcaption></figcaption></figure>

> Answer: _**2**_

***

* Then I did an exhaustive scan of the ports we found to get information about the running services

{% code lineNumbers="true" %}
```bash
nmap 10.129.1.138 -p22,27017 -sVC -oN serv_scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (54) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (595).png" alt=""><figcaption></figcaption></figure>

> Answer: _**MongoDB 3.6.8**_

***

<figure><img src="../../.gitbook/assets/image (598).png" alt=""><figcaption></figcaption></figure>

> Answer: _**NoSQL**_

***

<figure><img src="../../.gitbook/assets/image (599).png" alt=""><figcaption></figcaption></figure>

> Answer: _**mongosh**_

***

<figure><img src="../../.gitbook/assets/image (600).png" alt=""><figcaption></figcaption></figure>

> Answer: _**show dbs**_

***

<figure><img src="../../.gitbook/assets/image (601).png" alt=""><figcaption></figcaption></figure>

> Answer: _**show collections**_

***

<figure><img src="../../.gitbook/assets/image (602).png" alt=""><figcaption></figcaption></figure>

> Answer: _**db.flag.find().pretty()**_

***

* As we found a [_MongoDB_](https://www.mongodb.com/) database service running on port 27017, I tried connecting to the service using the utility [_mongosh_](../../database-attacks/tools-and-utilities.md#mongosh)_,_ and it worked successfully

{% code overflow="wrap" lineNumbers="true" %}
```bash
mongosh mongodb://10.129.1.138:27017
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (55) (1).png" alt=""><figcaption></figcaption></figure>

***

* Once inside, I checked for the existing databases and noticed a suspicious database named _sensitive\_information._ I accessed it and filtered the information it contained using the keyword _flag_ and got an object that contained this parameter, letting me know the root flag

<pre class="language-mongodb" data-overflow="wrap" data-line-numbers><code class="lang-mongodb"><strong>test> show dbs
</strong><strong>test> use sensitive_information
</strong>sensitive_information> db.flag.find().pretty()
</code></pre>

<figure><img src="../../.gitbook/assets/image (56) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (39) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**1b6e6fb359e7c40241b6d431427ba6ea**_
