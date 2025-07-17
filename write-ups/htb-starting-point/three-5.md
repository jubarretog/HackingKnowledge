# Tactics (Tier 1)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark>**&#x20;1**
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Windows
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Protocols / SMB / Reconnaissance / Misconfiguration

<figure><img src="../../.gitbook/assets/image (351).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* With a little research, I started answering the first questions

<figure><img src="../../.gitbook/assets/image (576).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-Pn**_

***

<figure><img src="../../.gitbook/assets/image (577).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Server Message Block**_

***

<figure><img src="../../.gitbook/assets/image (578).png" alt=""><figcaption></figcaption></figure>

> Answer: _**445**_

***

<figure><img src="../../.gitbook/assets/image (579).png" alt=""><figcaption></figcaption></figure>

> Answer: _**-L**_

***

<figure><img src="../../.gitbook/assets/image (580).png" alt=""><figcaption></figcaption></figure>

> Answer: _**$**_

***

* Then I did an initial scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.52.162 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (581).png" alt=""><figcaption></figcaption></figure>

***

* I also did an exhaustive scan to get more information about the services running on the open ports

<pre class="language-basic" data-line-numbers><code class="lang-basic"><strong>nmap 10.129.52.162 -p135,139,445 -sVC -oN serv_scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (582).png" alt=""><figcaption></figcaption></figure>

***

* I found the SMB protocol running on port 445, so I tried to interact with it. For that, I used the [_smbclient_](../../networks/tools-and-utilities.md#smbclient) utility specifying that I just wanted to list the contents and try to do it as the _Administrator_ user, as I knew that was a _Windows_ system. I also entered a blank password as I didn't know any credentials, and the execution was successful

{% code lineNumbers="true" %}
```bash
smbclient -L 10.129.52.162 -U Administrator 
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (583).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the SMB protocol, you can go [here](../../networks/protocols/smb.md)
{% endhint %}

***

* With this, I could try to access the folders on the server and check their content. I started looking into the _C$_ direction as it is typically the main route for the _Windows_ filesystem, once again, as the _Administrator_ user

{% code overflow="wrap" lineNumbers="true" %}
```bash
smbclient //10.129.52.162/C$ -U Administrator
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (343).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next questions

<figure><img src="../../.gitbook/assets/image (344).png" alt=""><figcaption></figcaption></figure>

> Answer: _**C$**_

***

<figure><img src="../../.gitbook/assets/image (345).png" alt=""><figcaption></figcaption></figure>

> Answer: _**get**_

***

<figure><img src="../../.gitbook/assets/image (346).png" alt=""><figcaption></figcaption></figure>

> Answer: _**psexec.py**_

***

* Once inside, I listed the contents of the folder, and as expected, I saw the folders related to the _Windows_ filesystem, so knowing this, I went to the _Users_ folder and listed all of its content too

<figure><img src="../../.gitbook/assets/image (348).png" alt=""><figcaption></figcaption></figure>

***

* There was a folder for the _Administrator_ user, so I tried accessing it and then going to the _Desktop_ to check. I listed the contents and found a _flag.txt_ file, so I downloaded it from the server and then closed the connection

<figure><img src="../../.gitbook/assets/image (349).png" alt=""><figcaption></figcaption></figure>

***

* Finally, I checked the content of the file and found the flag

<figure><img src="../../.gitbook/assets/image (350).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**f751c19eda8f61ce81827e6930a1f40c**_
