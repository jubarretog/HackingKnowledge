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

Here we can find some tools and utilities commonly used for processes related to information gathering:

## <mark style="color:green;">DNS Dumpster</mark>

* Web tool that maps a Domain through DNS services it uses.&#x20;
* [https://dnsdumpster.com/](https://dnsdumpster.com/)

## <mark style="color:green;">Shodan.io</mark>

* Online service that is built as a search engine for internet-connected devices.
* The utility tries to connect to every device reachable online, once it gets a response, it collects all the information related to the service and saves it in the database to make it searchable.
* [https://www.shodan.io/](https://www.shodan.io/)

## <mark style="color:green;">**Wayback Machine**</mark>

* A website that creates snapshots of pages in time and displays them to the user.
* [https://archive.org/web/](https://archive.org/web/)

## <mark style="color:green;">Wappalyzer</mark>

* A website that helps to determine what technologies a page uses. Also works as a Firefox extension.&#x20;
* Web site: [https://www.wappalyzer.com/](https://www.wappalyzer.com/)
* Firefox extension: [https://addons.mozilla.org/es/firefox/addon/wappalyzer/](https://addons.mozilla.org/es/firefox/addon/wappalyzer/)

## <mark style="color:green;">**User-Agent Switcher and Manager**</mark>&#x20;

* Gives you the ability to pretend to be accessing the webpage from a different operating system or different web browser
* [https://addons.mozilla.org/en-US/firefox/addon/user-agent-string-switcher/](https://addons.mozilla.org/en-US/firefox/addon/user-agent-string-switcher/)

## <mark style="color:green;">**OWASP Favicon**</mark>

* Database to identify typical icons of Development Frameworks
* [https://wiki.owasp.org/index.php/OWASP\_favicon\_database](https://wiki.owasp.org/index.php/OWASP\_favicon\_database)

## <mark style="color:green;">LinEnum</mark>&#x20;

* Another tool for Linux enumeration
* [https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum)

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
git clone https://github.com/rebootuser/LinEnum
```
{% endcode %}

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
