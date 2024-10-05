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

# Commands

In Windows, both Command Prompt (CMD) and PowerShell serve as powerful command-line interfaces that enable users to execute commands, manage system settings, and automate tasks. Therefore, it's important to be familiar with these utilities.

To help with that, below we can find a list of common and useful commands for both interfaces:

## <mark style="color:blue;">CMD Commands</mark>

* Show the name of the system.

<pre class="language-sh" data-overflow="wrap" data-line-numbers><code class="lang-sh"><strong>hostname
</strong></code></pre>

***

* Show the logged-in user.

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

* Show network address settings.

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

## <mark style="color:blue;">PowerShell Commands</mark>

* Here are the PowerShell commands

{% code overflow="wrap" lineNumbers="true" %}
```powershell
command $command
```
{% endcode %}
