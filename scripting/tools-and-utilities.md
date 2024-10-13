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

Here we can find some tools and utilities commonly used for processes related to scripting:

## <mark style="color:green;">Impacket</mark>&#x20;

Collection of Python classes for working with network protocols

### <mark style="color:yellow;">Commands</mark>

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
sudo impacket-mssqlclient  $user@$ip --windows-auth #Example for windows authentication in SQL server
```
{% endcode %}
