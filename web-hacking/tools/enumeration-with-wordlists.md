# Enumeration with wordlists

* Use Brute-Forcing to get hidden files, directorys and paths from a website
* Daniel Miessler Wordlists: [https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists)



## <mark style="color:green;">gobuster</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install gobuster
```
{% endcode %}

***

* Show commands and utilities

{% code overflow="wrap" lineNumbers="true" %}
```bash
gobuster -h
```
{% endcode %}

***

* Scan

{% code overflow="wrap" lineNumbers="true" %}
```bash
gobuster -u $URL #Scan url
gobuster -u $url-w $wordlist #Specify wordlist path
gobuster dir -u $url -w $wordlist #Directory and file mode
gobuster vhost $url -w $wordlist #Subdomain mode
gobuster vhost $url -w $wordlist --append-domain #To set de subdomain first
```
{% endcode %}

##

## <mark style="color:green;">ffuf</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install ffuf
```
{% endcode %}

***

* Scan

{% code overflow="wrap" lineNumbers="true" %}
```bash
ffuf -u $URL/FUZZ -w $wordlist #FUZZ to fill the part to be fuzz
ffuf -u $URL/FUZZ -w $wordlist -o $filename #get output in a file
```
{% endcode %}

{% hint style="info" %}
**Note:** Optional keywords can be added after `$wordlist` separating them with `,`&#x20;
{% endhint %}

##

## <mark style="color:green;">dirb</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install dirb
```
{% endcode %}

***

* Scan

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">dirb $URL #Scan url
dirb $URL $wordlist #Use wordlist
dirb $URL $wordlist -w #Ignore warning messages
dirb $URL $wordlist -u $username:$password #Use 
<strong>dirb $URL $wordlist -E $certificate  #Use certificate
</strong></code></pre>



## <mark style="color:green;">nikto</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install nikto
```
{% endcode %}

***

* Scan

{% code overflow="wrap" lineNumbers="true" %}
```bash
nikto -h $url
```
{% endcode %}
