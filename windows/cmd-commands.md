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

# CMD commands

* Show the name of the system.

<pre class="language-sh" data-overflow="wrap" data-line-numbers><code class="lang-sh"><strong>hostname
</strong></code></pre>

***

* Show the logged in user.

{% code overflow="wrap" lineNumbers="true" %}
```sh
whoami
```
{% endcode %}

***

* &#x20;Show manual for a command.

{% code overflow="wrap" lineNumbers="true" %}
```shell
$command /
```
{% endcode %}

***

* Show network adress settings.

{% code overflow="wrap" lineNumbers="true" %}
```bash
ipconfig
ipconfig /all    #Full configuration information
```
{% endcode %}

***

* Show protocol statistics and current TCP/IP network connections.

{% code overflow="wrap" lineNumbers="true" %}
```sh
netstat
```
{% endcode %}

***

* Makes a ping to a machine

{% code overflow="wrap" lineNumbers="true" %}
```sh
ping -n $IPadress
```
{% endcode %}

***

* Traces the route taken by the packets from your system to another host

{% code overflow="wrap" lineNumbers="true" %}
```bash
tracert $IPadress
```
{% endcode %}

***

