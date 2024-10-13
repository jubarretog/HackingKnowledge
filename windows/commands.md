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

In Windows, two built-in command-line interfaces allow users to execute commands, manage system settings, and automate tasks. It is important to be familiar with these utilities to fully leverage the potential of the operating system.

## <mark style="color:blue;">CMD</mark>

A command-line interpreter that allows users to execute commands from a text-based interface. It supports a wide range of commands for file manipulation, system configuration, and troubleshooting. Some of the commands that can be used through this interface are:

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

## <mark style="color:blue;">PowerShell</mark>

A command-line interpreter that supports a wide range of commands for automating administrative tasks, managing complex configurations, and interacting with web services or APIs.&#x20;

Integrates the .NET framework and offers advanced scripting capabilities. Some of the commands for this interface are:

* Retrieves a list of currently running processes

{% code overflow="wrap" lineNumbers="true" %}
```powershell
Get-Process
```
{% endcode %}

***

* Lists all services on the system and their current status

{% code overflow="wrap" lineNumbers="true" %}
```powershell
Get-Service
```
{% endcode %}

***

* Configures the execution policy, controlling the ability to run scripts

{% code overflow="wrap" lineNumbers="true" %}
```powershell
Set-ExecutionPolicy $option
```
{% endcode %}

***

* Displays detailed help information about commands, including usage examples

{% code overflow="wrap" lineNumbers="true" %}
```powershell
Get-Help $command
```
{% endcode %}

***

* Lists the files and directories in a specified location, similar to `dir` or `ls` in other systems.

{% code overflow="wrap" lineNumbers="true" %}
```powershell
Get-ChildItem $path
```
{% endcode %}

* Copies files or directories from one location to another.

{% code overflow="wrap" lineNumbers="true" %}
```powershell
Copy-Item -Path $path -Destination $destination
```
{% endcode %}

***

* Displays the content of a file, similar to `cat` in Linux.

{% code overflow="wrap" lineNumbers="true" %}
```powershell
Get-Content $filepath
```
{% endcode %}

***

* Creates a new file, directory, or other type of item.

{% code overflow="wrap" lineNumbers="true" %}
```powershell
New-Item -Path $path -ItemType $type
```
{% endcode %}