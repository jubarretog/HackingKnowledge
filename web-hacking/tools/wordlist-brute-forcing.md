# Wordlist Brute-Forcing

Use Brute-Forcing to get hidden files, directorys and paths from a website

* Daniel Miessler Wordlists [https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists)

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

* Scan specify URL

{% code overflow="wrap" lineNumbers="true" %}
```bash
gobuster -u $URL
```
{% endcode %}

***

* Start scanning

{% code overflow="wrap" lineNumbers="true" %}
```bash
gobuster -u $url-w $wordlist #Specify wordlist path
gobuster dir -u $url -w $wordlist #Directory and file mode
gobuster vhost $url -w $wordlist #Subdomain mode
gobuster vhost $url -w $wordlist --append-domain #To set de subdomain first
```
{% endcode %}

## <mark style="color:green;">ffuf</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install ffuf
```
{% endcode %}



* Use wordlist

{% code overflow="wrap" lineNumbers="true" %}
```bash
ffuf -u $URL -w $wordlist
ffuf -u $URL -w $wordlist -o $filename        #write output to a file
```
{% endcode %}

{% hint style="info" %}
**Note:** Optional keywords can be added in after `$wordlist` separating them with `,`&#x20;
{% endhint %}

## <mark style="color:green;">dirb</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install dirb
```
{% endcode %}



* Use wordlist

{% code overflow="wrap" lineNumbers="true" %}
```bash
dirb $URL $wordlist
dirb -w $URL $wordlist                      #Ignore warning messages
dirb -u $username:$password $URL $wordlist  #Use authentication
dirb -E $certificated $URL $wordlist        #Use a certificate for autenthication
```
{% endcode %}
