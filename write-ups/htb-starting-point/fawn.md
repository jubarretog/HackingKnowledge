# Fawn (Tier 0)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark> 0
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> FTP / Protocols / Reconnaissance / Anonymous-Guest Access

<figure><img src="../../.gitbook/assets/image (20) (1) (1) (1) (1).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=0">https://app.hackthebox.com/starting-point?tier=0</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* With a little research, I started answering the first questions

<figure><img src="../../.gitbook/assets/image (47) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**File Transfer Protocol**_

***

<figure><img src="../../.gitbook/assets/image (48) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**21**_

***

<figure><img src="../../.gitbook/assets/image (49) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**sftp**_

***

<figure><img src="../../.gitbook/assets/image (50) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ping**_

***

* Then I did an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code overflow="wrap" lineNumbers="true" %}
```sh
nmap -p- -Pn --min-rate 2000 10.129.92.84
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (46) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to get information on the services running on the found ports

{% code lineNumbers="true" %}
```bash
nmap -p- -Pn --min-rate 2000 10.129.92.84
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (52) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (51) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**vsftpd 3.0.3**_

***

<figure><img src="../../.gitbook/assets/image (54) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Unix**_

***

<figure><img src="../../.gitbook/assets/image (55) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ftp -h**_

***

<figure><img src="../../.gitbook/assets/image (56) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**anonymous**_

***

* I identified a port that was running the FTP protocol, so I could try connecting through this. As I didn't have any credentials, I tried logging in as an anonymous user, which wouldn't ask for a password, and with this, I successfully got in

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong>ftp 10.129.92.94
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (57) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (58) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the FTP protocol, you can go [here](../../networks/protocols/ftp/)
{% endhint %}

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (59) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**230**_

***

<figure><img src="../../.gitbook/assets/image (60) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**ls**_

***

<figure><img src="../../.gitbook/assets/image (61) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**get**_

***

* Once inside, I listed the files being shared on the FTP server and found a _flag.txt_ file. So I used the internal `get` command to download the _flag.txt_ file from the server, and then closed the connection

<figure><img src="../../.gitbook/assets/image (63) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (62) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

* Having it locally, I checked the content of the file, finally retrieving the root flag

<figure><img src="../../.gitbook/assets/image (64) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (65) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**035db21c881520061c53e0536e44f815**_
