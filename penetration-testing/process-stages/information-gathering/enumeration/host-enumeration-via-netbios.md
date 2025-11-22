# Host Enumeration via NetBIOS

On _Windows,_ we can get information about the hosts under a network by interacting with the NetBIOS protocol

* We can use it to obtain the name table of a remote machine

<pre class="language-powershell" data-overflow="wrap" data-line-numbers><code class="lang-powershell"><strong>nbtstat -a $hostname
</strong>nbtstat -a $IP
<strong>
</strong><strong>#Example output
</strong><strong>...
</strong><strong>Name               Type         Status
</strong>---------------------------------------------
WORKSTATION01  &#x3C;00>  UNIQUE      Registered
WORKGROUP      &#x3C;00>  GROUP       Registered    #Default group
WORKSTATION01  &#x3C;20>  UNIQUE      Registered
...
</code></pre>

***

* We could compare it to other hosts to identify if they are from the same or related domains, and even if they could belong to an Active Directory

<pre class="language-powershell" data-overflow="wrap" data-line-numbers><code class="lang-powershell"><strong>nbtstat -a $hostname
</strong><strong>
</strong><strong>#Example output
</strong><strong>...
</strong><strong>Name               Type         Status
</strong>---------------------------------------------
WORKSTATION02  &#x3C;00>  UNIQUE      Registered
DOMAIN         &#x3C;00>  GROUP       Registered    #Custom domain
WORKSTATION02  &#x3C;20>  UNIQUE      Registered
DOMAIN2        &#x3C;00>  GROUP       Registered    #Custom domain
...
</code></pre>

***

* We could also generate a list of recently resolved NetBIOS names and their corresponding IP addresses to build a custom routing table

<pre class="language-powershell" data-overflow="wrap" data-line-numbers><code class="lang-powershell"><strong>nbtstat -c
</strong><strong>
</strong><strong>#Example output
</strong><strong>...
</strong>Name               Type       Host Address    Life [sec]
--------------------------------------------------------
DOMAIN        &#x3C;00>  GROUP     192.168.1.10    543
WORKGROUP     &#x3C;00>  GROUP     192.168.1.255   340
...
</code></pre>

***

* We could also check shared resources using the `net view` commmand

<pre class="language-powershell" data-overflow="wrap" data-line-numbers><code class="lang-powershell"><strong>net view \\$IP /ALL
</strong><strong>
</strong><strong>#Example output
</strong><strong>...
</strong>Share name     Type   Used as  Comment
------------------------------------------
C$             Disk            Default share
SharedDocs     Disk            Shared documents     #Not default
...
</code></pre>
