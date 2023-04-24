# Tools

## <mark style="color:green;">Netcat</mark>

### **Characteristics**

* Unix utility which reads and writes data across network connections
* Can be used with TCP or UDP protocol

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
```
{% endcode %}



* Use only numeric IP no DNS

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -n $IP $port
```
{% endcode %}



* Verbose Output

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -v $hostname $port
```
{% endcode %}

***

* Start in listen mode in the specified port

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -l -p $Port
```
{% endcode %}



* Make a file transmission

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -lp $port > $incomingfile  #From listening side
nc -n -v - $port < $file      #From sender side
$incomingfile -h              #Check is trasmision was correct from listener side
```
{% endcode %}



*

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -l -p $Port -e $program
```
{% endcode %}



## <mark style="color:green;">Nmap</mark>

### **Charactetistics**

* Network Mapper, open source tool for network exploration and security auditing
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

* General syntax

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap $scantype $options $target
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
```
{% endcode %}

***

* UDP scan

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -sU $target
nmap -sU --top-po
rts $numberofports $target   #Specify the most common UDP ports
```
{% endcode %}

***

* Perform Ping Sweep

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -sn $targetIPranges
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

* Increase verbosity level of output

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -v $target
nmap -vv $target      #Level 2 verbosity, MOST recommended
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

* Select which port scan

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -p $port $target
nmap -p $port-port $target   #Select a range of ports
nmap -p- $target             #Scan all ports
```
{% endcode %}

***

* Activate a script from NSE library

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap --script=$scriptfile  $target
nmap --script=$category  $target  #Active all scripts in the category
nmap -p $port --script=$script --script-args $script.$arg='$argvalue'
```
{% endcode %}

***

* Search scripts in NSE

{% code overflow="wrap" lineNumbers="true" %}
```bash
grep $keyword /usr/share/nmap/scripts/script.db    #Using grep
ls -l /usr/share/nmap/scripts/*$keyword*           #Using ls
```
{% endcode %}

***

* Scan without pinging a port

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap $target -Pn
```
{% endcode %}

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
