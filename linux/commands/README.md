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

# Commands

* Create a bash instance

{% code overflow="wrap" lineNumbers="true" %}
```bash
bash
```
{% endcode %}

***

* Exit from a bash instance

{% code overflow="wrap" lineNumbers="true" %}
```bash
exit
```
{% endcode %}

***

* Change user password

{% code overflow="wrap" lineNumbers="true" %}
```bash
passwd
```
{% endcode %}

***

* See manual/documentation or found a command

{% code overflow="wrap" lineNumbers="true" %}
```bash
man $command
man -k $keyword        #Make search of command by a keyword
apropos $keyword       #Find a command by description
```
{% endcode %}

***

* Clean up the console content

{% code overflow="wrap" lineNumbers="true" %}
```bash
clear
```
{% endcode %}

***

* Shows the current logged in user

{% code overflow="wrap" lineNumbers="true" %}
```bash
whoami
```
{% endcode %}

***

* Get the hostname of the machine

{% code overflow="wrap" lineNumbers="true" %}
```bash
hostname
```
{% endcode %}

***

* Get information about the machine and system

{% code overflow="wrap" lineNumbers="true" %}
```bash
uname
uname -a #Print all information
```
{% endcode %}

{% hint style="info" %}
Information come in the following order separated by spaces

* kernel-name
* nodename
* kernel release
* kernel version
* machine architecture
* processor architecture
* hardware platform architecture
* operating system
{% endhint %}

***

* Executes a command with superuser(root) permises

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo $command
sudo -l #See what commands can use the user with sudo
```
{% endcode %}

***

* See user and group information

{% code overflow="wrap" lineNumbers="true" %}
```bash
id
id $username #Can be used with any user
```
{% endcode %}

***

* Show all files and directories in specified

{% code overflow="wrap" lineNumbers="true" %}
```bash
ls           #In actual directory
ls $path     #In path directory
ls -a        #Include hidden files
ls -1        #List each file in a single line
ls -l        #File permissions, associated user and groups, creation date and hour
ls -l -lr    #List and order in z-a order
ls -l -lt    #List and order by last modified
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
sudo chmod -R 777 $filename #Give all permission to everyone
```

***

* Shows Actual Working directory

{% code overflow="wrap" lineNumbers="true" %}
```bash
pwd
```
{% endcode %}

***

* Change directory to the specified path

{% code overflow="wrap" lineNumbers="true" %}
```bash
cd        #Redirect to the home directory
cd ~      #Redirect to the home directory
cd $path  #Redirect to the specified file
cd ../    #Redirect to the upper directory
```
{% endcode %}

***

* Get path of file by searching in directories defined at PATH

{% code overflow="wrap" lineNumbers="true" %}
```bash
which $filename
```
{% endcode %}

***

* Get path of file by searching in **locate.db**

{% code overflow="wrap" lineNumbers="true" %}
```bash
locate $filename
```
{% endcode %}

{% hint style="info" %}
**Note:** `locate.db` is a build in db of system files
{% endhint %}

***

* Update `locate.db` manually

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo updatedb
```
{% endcode %}

***

* List sockets statistics

{% code overflow="wrap" lineNumbers="true" %}
```bash
ss
```
{% endcode %}

***

* Use enviroment variables

{% code overflow="wrap" lineNumbers="true" %}
```bash
env                           #List current variables
$variablename=$value          #Created only in the current shell
export $variablename=$value   #Created globally
```
{% endcode %}

***

* List command history

{% code overflow="wrap" lineNumbers="true" %}
```bash
history
export HISTCONTROL=$value          #Set output format for history
export HISTIGNORE='$regex'         #Set ignore values for history
export HISTTIMEFORMAT='$options'   #Set time format for history
```
{% endcode %}

***

* Repeat a command based on history

{% code overflow="wrap" lineNumbers="true" %}
```bash
!$number   #Repeat the command with that number
!!         #Repeat last command used
```
{% endcode %}

***

* Open a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
open $filename
display $imagefile
```
{% endcode %}

***

* Asign a name for simplificated a command or redefine a command

{% code overflow="wrap" lineNumbers="true" %}
```bash
alias $name=$command
alias          #See all defined aliases
unalias $name  #Delete alias
```
{% endcode %}

***

* Output any text that we provide

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>echo $text
</strong></code></pre>

***

* Create a new directory

{% code overflow="wrap" lineNumbers="true" %}
```bash
mkdir $dirname
mkdir ${dirname1,dirname2}            #Create various folders
mkdir -p $dirname/{$subdir1,$subdir2} #Create a folder with subfolders
```
{% endcode %}

***

* Shows file content in command-line

{% code overflow="wrap" lineNumbers="true" %}
```bash
cat $file
cat $path  #File in the specified file path
head $filename #Shows 10 initial lines
head -n$number $filename #Shows the first $number lines
tail $filename #Shows 10 final lines
tail -n$number $filename #Shows the last $number lines
tail -f $filename #Shows appended lines as data grows
less $file #Less is lighter, charge one page of content at time
```
{% endcode %}

***

* Find a file or directory

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">find .                      #All files and directories from the actual directory
find /                      #All files and directories from root directory
find $path                  #All files and directories from specific directory
find . -name $filename      #Find by exact name
find . -name "*.$extension" #All files with the specified extension
find . -d $dir              #Only search directories
find . -f $dir              #Only search files
<strong>find . -perm $permissions   #Find by specified permissions
</strong>find . -group $groupname    #Find by group
find . -user  $username     #Find by owner
find . -size  $size$unit    #Find by exact size, c for bytes, M for MB
find . -size  +$size$unit   #Find by larger size than specified
find . -size  -$size$unit   #Find by smaller size than specified
find . -mtime $n            #Files modified in the last n days
find . -atime $n            #Files accesed in the last n days
<strong>find . -cmin $n             #Files changed in the last n minutes
</strong>find . -amin $n             #Files accesed in the last n minutes
find . 2>/dev/null          #Exclude files with no permissions
</code></pre>

{% hint style="info" %}
The `-perm` flag can recieve permission such as `777` or `a=x`
{% endhint %}

***

* Count the number of entries in a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
wc $filename      #Count number of lines, words and characters
wc -l $filename   #Count number of lines
wc -m $filename   #Count number of characters
wc -c $filename   #Count number of bytes
wc -w $filename   #Count number of words
wc $filename $filename #Count various file at time, show total
```
{% endcode %}

***

* Search through a file and shows any entries with the specified value

{% code overflow="wrap" lineNumbers="true" %}
```bash
grep "$text" $filename
grep -i "$text" $filename   #Ignore the value given
grep -v "$text" $filename   #Returns non-matching results
```
{% endcode %}

***

* Edit text and streams

{% code overflow="wrap" lineNumbers="true" %}
```bash
sed '$regex' $filename
```
{% endcode %}

***

* Extract a section of text from file

{% code overflow="wrap" lineNumbers="true" %}
```bash
cut -f $fieldnumber -d "$delimiter" $filename
awk -F "$delimiter" '{print $field, $field}'     #Extraction with AWK
```
{% endcode %}

***

* Sort lines of a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
sort $filename     #Order by alphabeth using first character
sort -f $filename  #Ignore Case sensitive
sort -u $filename  #Takes only first entry
sort -r $filename  #Reverse the result
sort -n $filename  #Compare as numerical value
sort -k $field$delimitertor$position frutas #Order by field and position
```
{% endcode %}

***

* Find unique ocurrencies in a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
sort $filename | uniq 
sort $filename | uniq -c #Count number of ocurrencys
sort $filename | uniq -b #Get repeated lines
```
{% endcode %}

{% hint style="info" %}
**Note:** `uniq` needs a sort file as input for work correctly
{% endhint %}

***

* Compare content of files

{% code overflow="wrap" lineNumbers="true" %}
```bash
comm $file1 $file2
comm -$number $file1 $file2  #Supress especified lines
diff $file1 $file2 
diff -c $file1 $file2     #Ouput in context format
diff -u $file1 $file2     #Ouput in unified format
```
{% endcode %}

{% hint style="info" %}
**Note:** In `comm` output first column Represents unique lines for first file, second columns the unique lines for second file, and the third column the lines both share.
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
gzip $filename                 #Compress
gzip -d $filename              #Extract
bzip2 $filename                #Compress
bzip2 -d $filename             #Extract
tar -f $filename               #Compress
tar -cvz $filename               #Compress
tar -xf $filename              #Extract
7z a $namecompressed $filename #Compress
7z e $filename                 #Extract
```
{% endcode %}

***

* Use data encryption

{% code overflow="wrap" lineNumbers="true" %}
```bash
gpg -e $filename               #Encrypt data
gpg -d $filename               #Decrypt data
```
{% endcode %}

***

* Access to a remote machine through ssh

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>ssh $user@$IP
</strong><strong>ssh -i $privatekey $user@$IP  #Connect with a private key
</strong>ssh -T $user@$IP              #Connect trying tunneling
</code></pre>

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
mv $filename $newname  #Rename file
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

* Execute a command at regular intervals

{% code overflow="wrap" lineNumbers="true" %}
```bash
watch
watch -n$number $command #Execute command every $number seconds
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
vi $filename      #More powerful Text Editor
vim $filename     #Improved version of vi
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

* Make petitions to websites

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>curl $URL #Make a get petition
</strong>curl -L $URL #Follow redirections
curl -O $URL/$file      #Save a file with same name
<strong>curl -o $name $URL/$file  #Save a file with a different name
</strong>curl -o $URL/$file1 -o $URL/$file2 #Get various files
curl $URL -d "$param=$value"  #Specificate values of body
curl -X $PETITION $URL #Make an specific type of petition
curl $firstpetition --next $secondpetition #Make variuos petition
curl $URL -H "$header:$value" #Specific header in a petition
curl $URL -v  #Get verbose output

wget $URL
wget -O $URL/file  #Save a file with same name
wget -o $name $URL/file  #Save a file with a different name

axel $URL           #Dowload through various connections
axel -n$number $URL #Specify number of connection to use
axel -O $name $URL  #Save with a different name
</code></pre>

***

* Codificate MD5 encryption for a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
md5sum $filename
```
{% endcode %}

***

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
ps                  #Show process run in the user sesion
ps aux              #Shows other user and complete system processes
ps -A               #Shows all processes
ps -f               #Display full format listing
ps -C $commandname  #Shows process with a specified command
ps axjf             #Show as a tree
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

* Manage system process and services

{% code overflow="wrap" lineNumbers="true" %}
```bash
systemctl $option $process
systemctl start $process       #For starting a process
systemctl stop $process        #For killing a process
systemctl enable $process      #Set proccess to start at startup
systemctl disable $process     #Set proccess to not start at startup
systemctl list-unit-files      #List status of services
```
{% endcode %}

***

* Foreground a process

{% code overflow="wrap" lineNumbers="true" %}
```bash
fg $PID
fg %$jobID    #Foreground specified list ID process
fg %$String   #Refers to the beginning of the suspended process
fg %+         #Refers to the current job
fg %-         #Refers to the previus job
```
{% endcode %}

***

* Background a process

{% code overflow="wrap" lineNumbers="true" %}
```bash
bg         #Resume stopped background processes
bg $PID   
```
{% endcode %}

{% hint style="info" %}
**Note:** Background can only be used after stopping a process with <mark style="color:orange;">`^z`</mark>
{% endhint %}

***

* List actual shell process

{% code overflow="wrap" lineNumbers="true" %}
```bash
jobs
```
{% endcode %}

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

* Manage packages, repositories and digital signature from APT

{% code overflow="wrap" lineNumbers="true" %}
```bash
apt install $packagename   #Install a package
apt reinstall $packagename #Reinstall a package from scratch
apt remove $packagename    #Remove a package
apt remove --purge $packagename  #Delete package and its configuration
apt update $packagename    #Update a package
apt update                 #Update all packages
apt upgrade                #Update linux system and applications
apt-get                    #Use first version for actions
apt-cache search $toolname #Search for a tool in apt repositories
apt show $packagename      #Show information about a package
add-apt-repository         #Add repositories from developers to your apt lists
apt-key add $filename      #Add key file to trusted keys list
apt-key del $keyID         #Remove key trusted keys list
apt-key list               #List all trusted keys
```
{% endcode %}

***

* Manage packages via Debian

```
dpkg -i $packagename   #Install a package 
dpkg -r $packagename   #Remove a package 
dpkg -P $packagename   #Delete package and its configuration
```

***

* Test if connection to a remote resource is possible

{% code overflow="wrap" lineNumbers="true" %}
```bash
ping $IPaddress
ping $URLdomain                 #Use domain name
ping $IPaddress -4              #Limit to only IPv4 requests
ping $IPaddress -6              #Limit to only IPv6 requests
ping $IPaddress -i $seconds     #Set time interval to send each packet
ping $IPaddress -v              #Show a verbose output
ping $IPaddress -c $number      #Send an exxact number of packet
ping $IPaddress -s $size        #Specify number of bytes of the data
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

{% hint style="info" %}
An `*` on response represent that a package hasn't got a ICMP message from router
{% endhint %}

***

* Shows domain register information

{% code overflow="wrap" lineNumbers="true" %}
```bash
whois $URLdomain
```
{% endcode %}

***

* Obtain IP and record information of a domain

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
dig $URLdomain $record
dig @$DNSIPaddress $URLdomain           #Look up DNS records
dig @$DNSIPaddress $URLdomain $record   #Specify record type on DNS records
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

***

* Network utilitis

{% code overflow="wrap" lineNumbers="true" %}
```bash
ifconfig     #Check network nterfaces
iwconfig     #Check only wireless Interfaces
ip route     #Check existing network routes
netstat      #Check ports and active connections
netstat -a   #List all ports and connection
netstat -l   #List listening ports
netstat -t   #List only tcp ports
netstat -u   #List only udp ports
netstat -s   #List network usage statistics by protocol
netstat -p   #List with PID and program name
netstat -ano #Most common use, n to no resolve names, o to display timers
```
{% endcode %}

{% hint style="info" %}
If with `netstat -p` the PID and name aren't shown it's because the process is owned by another user. Running the command with sudo could show this information
{% endhint %}

***

* List capabilities of all binany files

{% code overflow="wrap" lineNumbers="true" %}
```bash
getcap -r / 2>/dev/null #Is good practice to redirect errors if not run with sudo
```
{% endcode %}

***

