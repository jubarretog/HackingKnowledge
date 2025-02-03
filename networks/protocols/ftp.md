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

# FTP

**File Transfer Protocol** is a standard network protocol used for transferring files between a client and a server. It operates in the Application layer and uses various authentication methods, including username and password authentication.&#x20;

Similar to [Telnet](telnet.md), sends data in plain text, making it vulnerable to eavesdropping, supports different network configurations to handle firewalls and NAT. Uses usually port 21, known as Control Channel to handle commands and responses, and port 20, known as Data Channel, to transfer files.

## <mark style="color:green;">Command-line utility</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install ftp
```
{% endcode %}

***

* Connect using the protocol

{% code overflow="wrap" lineNumbers="true" %}
```bash
ftp $ip
name: anonymous #Stablish an anonymous connection
ftp:\>          #Text based interface
ftp:\> ls                          #List files on the server 
ftp:\> get $filename               #Download a file
ftp:\> mget $filename $filename2   #Download multiple files
ftp:\> mget *                      #Download all files
ftp:\> put $filename               #Upload a file
ftp:\> exit                        #Close connection
```
{% endcode %}
