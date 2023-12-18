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

## <mark style="color:green;">Impacket</mark>&#x20;

Collection of Python classes for working with network protocols

## Commands

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install python3-impacket
```
{% endcode %}

***

* Use of scripts

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo impacket-$scriptname -$flag
sudo impacket-mssqlclient  $user@$ip --windows-auth #Example for windows authentication in sql server
```
{% endcode %}

***

