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

# Tools

## <mark style="color:green;">SMBCLIENT</mark>

* Use of SMB Protocol to list directories and files remotely
* Commonly used in port 445

### **Commands**

* Start smb with IP

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo smbclient -I $IP
```
{% endcode %}

***

* List elements without password

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo smbclient -L $IP -I $IP -N
```
{% endcode %}

***

* Acces to a share instance

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo smbclient //$IP/$ShareName -N
```
{% endcode %}

***

* Execute a command

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo smbclient //$IP/$ShareName -N -c "$comand"
```
{% endcode %}

***

* Work in conection

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>smb: \> get $filename   #Download a file
</strong>smb: \> put $filename   #Upload a file
smb: \> exit            #Close conection
</code></pre>

***



## <mark style="color:green;">TELNET</mark>

* Use of Telnet Protocol
* Commonly used in port 23

### **Commands**

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
sudo telnet $ip 80 #We connect to http service
#We send a petition
GET / HTTP/1.1
host: telnet
#Then use enter twice to send
```
{% endcode %}

{% hint style="info" %}
If we don't specify host, we will get an error&#x20;
{% endhint %}

***

* Close conection

{% code overflow="wrap" lineNumbers="true" %}
```bash
telnet: \> exit
```
{% endcode %}

***



## <mark style="color:green;">FTP</mark>

* Use of FTP Protocol
* Commonly used in port 21

### **Commands**

* Start ftp

{% code overflow="wrap" lineNumbers="true" %}
```bash
ftp $ip
name: anonymous #Stablish anonymous conection
```
{% endcode %}

***

* Work with files

{% code overflow="wrap" lineNumbers="true" %}
```bash
ftp:\> get $filename   #Download a file
ftp:\> put $filename   #Upload a file
ftp:\> exit         #Close conection
```
{% endcode %}

***



## <mark style="color:green;">Netcat</mark>

* Unix utility which reads and writes data across network connections
* Can act as a server or as a listener server
* By default makes an TCP conection but can be used with TCP or UDP protocol

### **Commands**

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
$incomingfile -h                #Check is trasmision was correct from listener side
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
sudo nc $ip 80 #We connect to http service
#We send a petition
GET / HTTP/1.1
host: netcat
#Then use enter to send
```
{% endcode %}

{% hint style="info" %}
To make a line jump is neccesare press `SHIFT+ENTER`
{% endhint %}

***



## <mark style="color:green;">Nmap</mark>

* Network Mapper
* Open source tool for network exploration and security auditing
* Output is a list of scanned targets

### **NSE**

* Nmap Scripting Engine https://nmap.org/nsedoc/
* Library of scriptS in _Lua_ that can be used from scanning for vulnerabilities to automating exploits for them
* Every script has a category
* By default nmap stores scripts in _/usr/share/nmap/scripts/script.db_

### **Scan types**

* _SYN_ scans are also known as _Half-open_ or _stealth_, they are stealther tha _Connect_ scans
* The difference between _Connect_ and _SYN_ scan is that _SYN_ perform a full three-way handshake with the target, _SYN_ scans sends back a _RST_ packet after receiving a _SYN/ACK_.
* UDP scans are slower than TCP scans
* In UDP scans if port is open it will send no response and sill be markered as _open|filtered_. If there's a response will be markered as _open_. If is closed, the target responds with an ICMP packet containing a message that the port is unreachable.
* _NULL_, _FIN_, _Xmas_ are stealthier than _SYN_ or UDP scans, usually used for firewall evasion.
* _NULL_ scans send a TCP request with no flags, the target host responds with _RST_ if the port is closed.
* _FIN_ scans send a TCP request with FIN flag, used to gracefully close an active connection, the target host responds with _RST_ if the port is closed.
* _Xmas_ scans send a malformed TCP packet, the target host responds with _RST_ if the port is closed.
* Microsoft windows may respond to a _NULL_, _FIN_ or _Xmas_ scan with a _RST_ for every port.

### **Commands**

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
nmap $domain  #Scan an IP usign domain
nmap $ip1 $ip2  # Scan some IPs
nmap x.x.x.$range1-$range2 #Scan a range of IPs
nmap x.x.x.x/$mask  #Scan using CIDR notation
nmap -iL $inputfile #Scan using the IPs form a list
nmap -iR $number #Scan random hosts
nmap --exclude $ip  #Scan excluding an specific IP
nmap --excludefile $file #Scan excludings the IPs from a list
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
sudo nmap -sn -PM $target #Make adress mask request
sudo nmap -sn -PS $ports $target #Use TCP SYN ping
sudo nmap -sn -PA $ports $target #Use TCP ACK ping
sudo nmap -sn -PU $ports $target #Use UDP ping
</code></pre>

{% hint style="info" %}
* If _ICMP_ scans return MAC adresses means the hosts are in the same subnet
* Ports in TCP scans are optional
{% endhint %}

***

* DNS resolution

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo nmap -n #Don't use reverse-dns
sudo nmap -R #Use reverse-dns even with offline hosts
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

* Version of services running

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -sV $target
```
{% endcode %}

***

* List hosts to be scanned witouth scanning them

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

* Use scripts from NSE library

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>nmap -sC $target    #Script scan
</strong><strong>nmap --script=$scriptfile  $target
</strong>nmap --script=$category  $target  #Active all scripts in the category
nmap -p $port --script=$script --script-args $script.$arg='$argvalue' #Pass arguments to a script
#Search scripts
grep $keyword /usr/share/nmap/scripts/script.db    #Using grep
ls -l /usr/share/nmap/scripts/*$keyword*           #Using ls
</code></pre>

***

* Fragment packets sent in scan

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

* Specify delay between packects sent

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

***



## <mark style="color:green;">ARP-Scan</mark>

* Tool for making host discovery via ARP packets
* Only Devices in the same subnet can be discoveres via ARP

### **Commands**

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
arp-scan $tagetRange -I $netInterface #Specify wich network interface to use
```
{% endcode %}

***



## <mark style="color:green;">Masscan</mark>

* Tool for making port scaning
* More agresive than _arp-scan_

### **Commands**

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

***

