# Tools and Utilities

Here we can find some tools and utilities commonly used for processes related to information gathering:

## <mark style="color:green;">DNS Dumpster</mark>

* A web tool that maps a domain through the DNS services it uses
* [https://dnsdumpster.com/](https://dnsdumpster.com/)

## <mark style="color:green;">DNSrecon</mark>

* A tool to perform a general enumeration of a domain

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install dnsrecon
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
dnsrecon -h #Get help with use
dnsrecon -d $domain #Enumerate a domain
dnsrecon -n $nameserver #Enumerate a name server
dnsrecon -d $domain -t $type #Specify the type of enumeration
```
{% endcode %}

## <mark style="color:green;">Shodan</mark>

* An online service that is built as a search engine for internet-connected devices
* The utility tries to connect to every device reachable online. Once it gets a response, it collects all the information related to the service and saves it in the database to make it searchable
* [https://www.shodan.io/](https://www.shodan.io/)

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install shodan
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
shodan init $APIkey #Set API key from your Shodan account
shodan host $IP     #Search information about a host
```
{% endcode %}

## <mark style="color:green;">**Wayback Machine**</mark>

* A website that creates snapshots of pages in time and displays them to the user
* [https://archive.org/web/](https://archive.org/web/)

## <mark style="color:green;">Wappalyzer</mark>

* A website that helps to determine what technologies a page uses. Also works as a Firefox extension
* Website: [https://www.wappalyzer.com/](https://www.wappalyzer.com/)
* Firefox extension: [https://addons.mozilla.org/es/firefox/addon/wappalyzer/](https://addons.mozilla.org/es/firefox/addon/wappalyzer/)

## <mark style="color:green;">**User-Agent Switcher and Manager**</mark>&#x20;

* Gives you the ability to pretend to be accessing the webpage from a different operating system or different web browser
* [https://addons.mozilla.org/en-US/firefox/addon/user-agent-string-switcher/](https://addons.mozilla.org/en-US/firefox/addon/user-agent-string-switcher/)

## <mark style="color:green;">**OWASP Favicon**</mark>

* Database to identify typical icons of Development Frameworks
* [https://wiki.owasp.org/index.php/OWASP\_favicon\_database](https://wiki.owasp.org/index.php/OWASP_favicon_database)

## <mark style="color:green;">LinEnum</mark>&#x20;

* Another tool for Linux enumeration
* [https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum)

### <mark style="color:yellow;">Commands</mark>

* Installation

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>git clone https://github.com/rebootuser/LinEnum
</strong></code></pre>

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
./LinEnum.sh -s -k keyword -r report -e /tmp/ -t
```
{% endcode %}

## <mark style="color:green;">Spiderfoot</mark>

* Open-source intelligence (OSINT) automation tool
* [https://github.com/smicallef/spiderfoot](https://github.com/smicallef/spiderfoot)

### <mark style="color:yellow;">Usage</mark>

* Click the _New Scan_ tab, enter a name for the scan, and select a target. Scanning can also be personalized by the type of information required or by choosing the individual scanner modules
* To add API keys, go to the _Settings_ tab, open the page for the module you are looking for, and complete the table, including the type of information the module searches for
  * If you don't know how to get the API keys, click the `?` next to the _API_ option in the module and follow the instructions to get API keys

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install spiderfoot
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
spiderfoot -l 127.0.0.1:$port    #Deploy app locally in the specified port
spiderfoot -M                    #Display available modules
```
{% endcode %}

## <mark style="color:green;">OSINT Framework</mark>

* OSINT Framework with several tools to gather information passively
* [https://osintframework.com/](https://osintframework.com/)

## <mark style="color:green;">Hunter.io</mark>

* Professional tool designed to help users find and verify email addresses associated with businesses or domains
* [https://hunter.io](https://hunter.io)

## <mark style="color:green;">Intelligence X</mark>

* OSINT search engine designed for searching leaked data, darknet content, and public records. It does its snapshots of some sites, being useful to search deleted or previously indexed sites
* [https://intelx.io](https://intelx.io)

## <mark style="color:green;">The Ultimate OSINT Collection</mark>

* Comprehensive, curated resource hub for open-source intelligence (OSINT) enthusiasts, investigators, and cybersecurity professionals
* [https://start.me/p/DPYPMz/the-ultimate-osint-collection](https://start.me/p/DPYPMz/the-ultimate-osint-collection?locale=es)

## <mark style="color:green;">Recon-ng</mark>

* OSINT framework that consists of a series of modules that can be run in workspaces

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install recon-ng
```
{% endcode %}

***

* Usage

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">recon-ng    #Initiate command interface
recon-web   #Initiate web GUI

#Inside the recon-ng console environment
[recon-ng][default] > help
[recon-ng][default] > workspaces create $wsname #Create workspace
[recon-ng][default] > workspaces list #List created workspaces
[recon-ng][default] > shell $command #Execute shell commands
<strong>[recon-ng][default] > back #Exit current context
</strong><strong>[recon-ng][default] > marketplace search #Check modules available
</strong>[recon-ng][default] > marketplace search $name #Search specific modules
[recon-ng][default] > marketplace refresh #Refresh available modules
[recon-ng][default] > marketplace info $name #Check about an specific module
[recon-ng][default] > marketplace install $name #Install a module
[recon-ng][default] > modules search #Check installed modules
[recon-ng][default] > modules load $name #Enter the context of a module to use it

#Inside the context of a module
[recon-ng][$module] > info #Get details about a module
[recon-ng][$module] > options set $option #Set parameters for a module
[recon-ng][$module] > run #Set parameters for a module
[recon-ng][$module] > dashboard #Get results of the information gathered
recon-ng][$module] > show $entry #Check for specific categories
</code></pre>

## <mark style="color:green;">Whatweb</mark>

* A tool to extract web servers, supporting frameworks, and applications

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install whatweb
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
whatweb $IPsslscan skillsforall.com
```
{% endcode %}

## <mark style="color:green;">crt.sh</mark>

* Obtain detailed certificate transparency information about a given domain
* [https://crt.sh/](https://crt.sh/)

## <mark style="color:green;">sslscan</mark>

* Command-line tool for testing and analyzing SSL/TLS-enabled services, checking their configuration and security

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install sslscan
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
sslscan $domain
```
{% endcode %}

## <mark style="color:green;">enum4linux-ng</mark>

* Command-line tool for doing reconnaissance and enumeration on _Linux_ hosts

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install enum4linux-ng
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
enum4linux-ng $IP
enum4linux-ng -A $IP #Do all simple enumeration
```
{% endcode %}

## <mark style="color:green;">SET</mark>

* Social Engineering Toolkit, an open-source penetration testing framework designed for social engineering. Has many custom attack vectors that allow you to make a believable attack quickly

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install set
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
setoolkit     #Launch
```
{% endcode %}

## <mark style="color:green;">emkei.cz</mark>

* An online tool for sending fake emails, useful for phishing attacks
* [https://emkei.cz](https://emkei.cz)

## <mark style="color:green;">BeEF</mark>

* Browser Exploitation Framework, a tool that can be used to manipulate users by leveraging XSS vulnerabilities via sending fake notifications and stealing cookies, among others

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install beef-xss
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
beef-xss 
```
{% endcode %}

## <mark style="color:green;">Censys</mark>

* Tool used for passive reconnaissance to find information about devices and networks on the Internet
* [https://censys.io](https://censys.io)

## [<mark style="color:green;">domain.glass</mark>](https://domain.glass/)

* Offers free DNS record, IP address, hostname, and WHOIS lookup information, providing transparent domain information
* [https://domain.glass/](https://domain.glass/)

## <mark style="color:green;">GrayHatWarfare</mark>

* Provides a search engine for publicly accessible Amazon S3 buckets, allowing users to search for open storage buckets that may contain sensitive files, misconfigurations, or exposed data
* [https://buckets.grayhatwarfare.com/](https://buckets.grayhatwarfare.com/)

## <mark style="color:green;">DNSenum</mark>

* A tool for information gathering and brute forcing of DNS domains and subdomains

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install dnsenum
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
dnsenum --enum $domain -f $wordlist -r # Bruteforce domain recursively
dnsenum --dnsserver $DNSip --enum $domain -f $wordlist #To use the Domain IP
dnsenum --enum $domain -f $wordlist -o $outFile #Specify an output file
dnsenum --dnsserver $DNSip --enum $domain -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -o $outFile #Recommended way
```
{% endcode %}

## <mark style="color:green;">wafw00f</mark>

* A tool used to detect the presence of a WAF on a web application

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
pip install git+https://github.com/EnableSecurity/wafw00f
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
wafw00f $domain
```
{% endcode %}

## <mark style="color:green;">Scrapy</mark>

* Custom scraper tailored for reconnaissance written in Python

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
pip install scrapy
mkdir Scrapy && cd ./Scrapy
wget -O ReconSpider.zip https://academy.hackthebox.com/storage/modules/144/ReconSpider.v1.2.zip
unzip ReconSpider.zip
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
python3 ReconSpider.py http://inlanefreight.com #Run the crawler
cat results.json #Check results
```
{% endcode %}

## <mark style="color:green;">FinalRecon</mark>

* Python-based reconnaissance tool with modules for different tasks like SSL certificate checking, Whois information gathering, header analysis, and crawling

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install finalrecon
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
finalrecon --headers --url $url #Get headers information
finalrecon --whois --url $url #Get whois lookup information
finalrecon --crawl --url $url #Crawl target
```
{% endcode %}
