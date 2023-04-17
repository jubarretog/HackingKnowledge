# Commands

* Clean up the console content

{% code overflow="wrap" lineNumbers="true" %}
```bash
clear
```
{% endcode %}



* Output any text that we provide

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>echo $text
</strong></code></pre>

***

* Shows the current logged in user

{% code overflow="wrap" lineNumbers="true" %}
```bash
whoami
```
{% endcode %}

***

* Executes a command with superuser(root) permises

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo $command
```
{% endcode %}

***

* Show all files and directories in specified

{% code overflow="wrap" lineNumbers="true" %}
```bash
ls           #In actual directory
ls $path     #In path directory
ls -a        #Include hidden files
ls -l        #File permissions, associated user and groups, creation date and hour
```
{% endcode %}

{% hint style="info" %}
**Note:** Hidden files start with a dot.  **Ex:**_`.hiddenfile`_
{% endhint %}

***

* Change permission of a file

```bash=
sudo chmod +$permision $filename  #Add permission
sudo chmod -$permision $filename  #Remove permission
```

***

* Change directory to the specified path

{% code overflow="wrap" lineNumbers="true" %}
```bash
cd        #Redirect the home directory
cd $path  #Redirect to the specified file
cd ../    #Redirect to the upper directory
```
{% endcode %}

***

* Shows file content in command-line

{% code overflow="wrap" lineNumbers="true" %}
```bash
cat $file
cat $path     #In the specified file path
```
{% endcode %}

***

* Shows Actual Working directory

{% code overflow="wrap" lineNumbers="true" %}
```bash
pwd
```
{% endcode %}

***

* Shows path where is the specified file

{% code overflow="wrap" lineNumbers="true" %}
```bash
find -name $filename
find *.$extension          #All paths to files with the specified extension
find -group $groupname     #Find by group
find -user  $username      #Find by owner
find -size  $size$unit     #Find by size
```
{% endcode %}

***

* Count the number of entries in a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
wc $filename
```
{% endcode %}

***

* Search through a file and shows any entries with the specified value

{% code overflow="wrap" lineNumbers="true" %}
```bash
grep "$text" $filename
```
{% endcode %}

***

* Sort lines of a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
sort $filename     #Ordena alfabeticamente por el primer caracter
sort -k $campo$separador$posicion frutas #Ordena por campo y posicion dados
```
{% endcode %}

***

* Find unique ocurrencies in a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
sort $filename | uniq 
sort $filename | uniq -c #Count number of ocurrencys
```
{% endcode %}

{% hint style="info" %}
**Note:** Uniq needs a sort file as input for work correctly
{% endhint %}

***

* Shows the content of a file with specifications

{% code overflow="wrap" lineNumbers="true" %}
```bash
tr $filename $expression
tr $filename -c $expression #Select the complement of expression
tr $filename -d $expression #Delete what concidies with expression
```
{% endcode %}

***

* Encode or decode base64

{% code overflow="wrap" lineNumbers="true" %}
```bash
base64 $filename -e        #Encode
base64 $filename -d        #Decode
```
{% endcode %}

***

* Transform hexdump

{% code overflow="wrap" lineNumbers="true" %}
```bash
xdd $filename        #Show hexdump of the file
xdd -r $filename     #Reverse hexdump to a file
```
{% endcode %}

***

* Compress or extract files

{% code overflow="wrap" lineNumbers="true" %}
```bash
gzip $filename            #Compress
gzip -d $filename         #Extract
bzip2 $filename           #Compress
bzip2 -d $filename        #Extract
tar -f $filename          #Compress
tar -xf $filename         #Extract
```
{% endcode %}

***

* Access to a remote machine through ssh

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>ssh $user@$IP
</strong><strong>ssh -i $privatekey $user@$IP  #Connect with a private key
</strong>ssh -T $user@$IP              #Connect trying tunneling
</code></pre>

***

* See manual/documentation for a command

{% code overflow="wrap" lineNumbers="true" %}
```bash
man $command
```
{% endcode %}

***

* Create a file with the specified name

{% code overflow="wrap" lineNumbers="true" %}
```bash
touch $filename
```
{% endcode %}

***

* Delete a file or directory

{% code overflow="wrap" lineNumbers="true" %}
```bash
rm $filename       #To remove a file
rm -R $dirname     #To remove a directory
```
{% endcode %}

***

* Copy the content of a file into a new one

{% code overflow="wrap" lineNumbers="true" %}
```bash
cp $filename $newfilename
```
{% endcode %}

***

* Move or rename a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
mv $filename $dirname
mv $filename $newname
```
{% endcode %}

***

* Shows the type of a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
file $filename
```
{% endcode %}

***

* Shows the initial lines of a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
head $filename
head -n $number $filename #Shows the first $number lines
```
{% endcode %}

***

* Change to the specified user

{% code overflow="wrap" lineNumbers="true" %}
```bash
su $username     #Change user and stay in the same place
su -l $username  #Redirects to the home directory of the other user
```
{% endcode %}

***

* Create or edit a file in command-line

{% code overflow="wrap" lineNumbers="true" %}
```bash
nano $filename
nano -B $filename #Make a backup when opening a file with nano
vim $filename     #More powerful Text Editor
```
{% endcode %}

{% hint style="info" %}
**Note:** In Unix `^` represents Ctrl key
{% endhint %}

***

* Shows stimate disk usage of a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
du $filename
du -h $filename    #Shows output in human-readable mode
du -b $filename    #Shows output in bytes mode
```
{% endcode %}

***

* Download files from the web via HTTP

{% code overflow="wrap" lineNumbers="true" %}
```bash
wget URL
curl $URL 
```
{% endcode %}



- ***

{% code overflow="wrap" lineNumbers="true" %}
```bash
md5sum $filename
```
{% endcode %}



* Get and Send files via SCP

{% code overflow="wrap" lineNumbers="true" %}
```bash
scp $filename $user@$remoteIP:$remotepath     #For sending a file
scp $user@$remoteIP:$remotepath $filename     #For getting a file
scp -r $dirname $user@$remoteIP:$remotepath   #For copying a directory
```
{% endcode %}

***

* Execute python utilities

{% code overflow="wrap" lineNumbers="true" %}
```bash
python3 $filename         #Execute a python file
python3 -m $modulename    #Start a python module
```
{% endcode %}

***

* Get information about the system running processes

{% code overflow="wrap" lineNumbers="true" %}
```bash
ps        #Show process run in the user sesion
ps aux    #Shows other user and complete system processes
```
{% endcode %}

***

* Get real time information about the system running processes

{% code overflow="wrap" lineNumbers="true" %}
```bash
top
```
{% endcode %}

***

* Kill a system proccess, we can send some signals to specified type of killing

{% code overflow="wrap" lineNumbers="true" %}
```bash
kill $PID
kill -s SIGTERM $PID   #Kill the process, but allow  to do some cleanup
kill -s SIGKILL $PID   #Kill the process but doesn't do any cleanup
kill -s SIGSTOP $PID   #Stop/suspend a process
```
{% endcode %}

{% hint style="info" %}
**Note** Proccess with a PID equal to 0 is a proccess that start with system boot
{% endhint %}

***

* Start or kill a process

{% code overflow="wrap" lineNumbers="true" %}
```bash
systemctl $option $process
systemctl start $process       #For starting a process
systemctl stop $process        #For killing a process
```
{% endcode %}

{% hint style="info" %}
**Note** There are other options like `unable` or `disable` etc...
{% endhint %}

***

* Foreground a process

{% code overflow="wrap" lineNumbers="true" %}
```bash
fg $PID
```
{% endcode %}

***

* Background a process

{% code overflow="wrap" lineNumbers="true" %}
```bash
bg $PID
```
{% endcode %}

{% hint style="info" %}
**Note:** Background can only be used after stopping a process with <mark style="color:orange;">`^z`</mark>
{% endhint %}

***

* Schedule to repeat a process as a crontab

{% code overflow="wrap" lineNumbers="true" %}
```bash
crontab -e     #Edit actual crontab
crontab -l     #Show actual crontab
crontab -r     #Delete actual crontab
crontab -i     #Prompt actual crontab and delete it
```
{% endcode %}

{% hint style="info" %}
**Note:** Every user has only one crometab
{% endhint %}

***

* Manage packages, repositories and digital signature

{% code overflow="wrap" lineNumbers="true" %}
```bash
apt-get install $packagename   #Install a package
apt-get reinstall $packagename #Reinstall a package from scratch
apt-get remove $packagename    #Remove a package
apt-get update $packagename    #Update a package
apt-get update                 #Update all package
apt-get upgrade                #Update linux system
add-apt-repository   #Add repositories from developers to your apt lists
apt-key add $filename    #Add key file to trusted keys list
apt-key del $keyID       #Remove key trusted keys list
apt-key list $filename   #Lisr all trusted keys
```
{% endcode %}

***

* Test if connection to a remote resource is possible

{% code overflow="wrap" lineNumbers="true" %}
```bash
ping $IPaddress
ping $URLdomain
ping $IPaddress -4              #Limit to only IPv4 requests
ping $IPaddress -6              #Limit to only IPv6 requests
ping $IPaddress -i $seconds     #Set time interval to send each package
ping $IPaddress -v              #Show a verbose output
```
{% endcode %}

***

* Show the path a request takes as it heads to the target machine

{% code overflow="wrap" lineNumbers="true" %}
```bash
traceroute $IPaddress
traceroute $URLdomain
traceroute $IPaddress -i $interface #Specify interface for send packets
traceroute $IPaddress -T #Use TCP SYN for connection probes
```
{% endcode %}

***

* Shows domain register information

{% code overflow="wrap" lineNumbers="true" %}
```bash
whois $URLdomain
```
{% endcode %}



* Obtain IP and record informationof a domain

{% code overflow="wrap" lineNumbers="true" %}
```bash
nslookup $URLdomain
nslookup -type=$record $URLdomain    #Specify record type
```
{% endcode %}

***

* Query recursive DNS servers for domain's information

{% code overflow="wrap" lineNumbers="true" %}
```bash
dig @$DNSIPaddress $URLdomain
dig @$DNSIPaddress $URLdomain  $record   #Specify record type
```
{% endcode %}

***

* Manage disk partition table

{% code overflow="wrap" lineNumbers="true" %}
```bash
fdisk $device
fdisk -l $device       #List all current disk partitions
```
{% endcode %}
