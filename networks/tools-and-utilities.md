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

Here we can find some tools and utilities commonly used for practices related to networks:

## <mark style="color:green;">Openvpn</mark>

* Tool for connecting to a VPN

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

## <mark style="color:green;">SMBclient</mark>

* Tool for accessing a server via SMB protocol

### <mark style="color:yellow;">**Commands**</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install smbclient
```
{% endcode %}

***

* Connect to an SMB server with the IP address

{% code overflow="wrap" lineNumbers="true" %}
```bash
smbclient -I $IP
```
{% endcode %}

***

* List elements without password

{% code overflow="wrap" lineNumbers="true" %}
```bash
smbclient -L $IP -I $IP -N
```
{% endcode %}

***

* Access to a shared instance

{% code overflow="wrap" lineNumbers="true" %}
```bash
smbclient //$IP/$ShareName -N
```
{% endcode %}

***

* Execute a command

{% code overflow="wrap" lineNumbers="true" %}
```bash
smbclient //$IP/$ShareName -N -c "$comand"
```
{% endcode %}

***

* Work in connection

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>smb: \> get $filename   #Download a file
</strong>smb: \> put $filename   #Upload a file
smb: \> exit            #Close connection
</code></pre>

## <mark style="color:green;">Telnet</mark>

* &#x20;Utility for using the Telnet protocol

### <mark style="color:yellow;">**Commands**</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install telnet
```
{% endcode %}

***

* Start telnet

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo telnet $ip $port
```
{% endcode %}

***

* Example

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo telnet $ip 80 #We connect to HTTP service
#We send a petition
GET / HTTP/1.1
host: telnet
#Then use enter twice to send
```
{% endcode %}

{% hint style="info" %}
If we don't specify the host, we will get an error&#x20;
{% endhint %}

***

* Close connection

{% code overflow="wrap" lineNumbers="true" %}
```bash
telnet: \> exit
```
{% endcode %}

## <mark style="color:green;">FTP</mark>

* Utility for using the FTP protocol

### <mark style="color:yellow;">**Commands**</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install ftp
```
{% endcode %}

***

* Start ftp

{% code overflow="wrap" lineNumbers="true" %}
```bash
ftp $ip
name: anonymous #Stablish an anonymous connection
```
{% endcode %}

***

* Work with files

{% code overflow="wrap" lineNumbers="true" %}
```bash
ftp:\> get $filename   #Download a file
ftp:\> put $filename   #Upload a file
ftp:\> exit         #Close connection
```
{% endcode %}

## <mark style="color:green;">Netcat</mark>

* Unix utility which reads and writes data across network connections
* Can act as a server or as a listener server
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

* Start in listen mode in the specified port

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -l -p $Port
nc -vnlp $Port     #Best way to make it
```
{% endcode %}

***

* Make a file transmission

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -vnlp $port > $incomingfile  #From listening side
nc -n -v - $port < $file        #From sender side
$incomingfile -h    #Check if the transmission was correct from the listener side
```
{% endcode %}

***

* Excute a program

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -l -p $Port -e $program
```
{% endcode %}

***

* Example

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo nc $ip 80 #We connect to HTTP service
#We send a petition
GET / HTTP/1.1
host: netcat
#Then use enter to send
```
{% endcode %}

{% hint style="info" %}
To make a line jump is necessary to press `SHIFT+ENTER`
{% endhint %}

## <mark style="color:green;">Nmap</mark>

* Open source tool for network exploration and security auditing which works as a network mapper

### <mark style="color:yellow;">**NSE**</mark>

* The [Nmap Scripting Engine](https://nmap.org/nsedoc/) is a library of scripts written in Lua that can be used for scanning vulnerabilities and automating exploits for them.
* Every script has a category related to its use scenario
* By default nmap stores scripts in _/usr/share/nmap/scripts/script.db_

### <mark style="color:yellow;">**Scan types**</mark>

* _SYN_ scans are also known as _Half-open_ or _Stealth._ They are stealthier than _Connect_ scans.
* The difference between _Connect_ and _SYN_ scans is that _Connect_ performs a full three-way handshake with the target. Instead of that _SYN_ scans send back an _RST_ packet after receiving an _SYN/ACK_.
* The UDP scans are slower than TCP scans.
* In UDP scans if the port is open it will send no response and will be marked as _open|filtered_. If there's a response will be marked as _open_. If is closed, the target responds with an ICMP packet containing a message that the port is unreachable.
* _NULL_, _FIN_, and _Xmas_ are stealthier than _SYN_ or UDP scans, usually used for firewall evasion.
* _NULL_ scans send a TCP request with no flags, the target host responds with _RST_ if the port is closed.
* _FIN_ scans send a TCP request with the _FIN_ flag, used to gracefully close an active connection, the target host responds with _RST_ if the port is closed.
* _Xmas_ scans send a malformed TCP packet, and the target host responds with _RST_ if the port is closed.
* Microsoft Windows may respond to a _NULL_, _FIN_ or _Xmas_ scan with a _RST_ for every port.

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

* Perform Ping Sweep (without pinging a port)

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
* If _ICMP_ scans return MAC addresses means the hosts are in the same subnet
* Ports in TCP scans are optional
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

{% hint style="info" %}
**Note:** This mode is louder than normal
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

{% hint style="info" %}
**Note:** Length must be a multiple of 8
{% endhint %}

***

* Specify delay between packets sent

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

* Tool for making host discovery via ARP packets
* Only devices in the same subnet can be discovered via ARP

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

* Tool for making port scanning
* Optimized for speed, making it particularly useful for large-scale scans

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
masscan $targetRange ‐‐top-ports $n    #Scan the n most used ports
```
{% endcode %}

## <mark style="color:green;">Docker</mark>

* Help to build, share, and run container applications.

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
