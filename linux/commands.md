# Commands

* Create a bash instance

{% code overflow="wrap" lineNumbers="true" %}
```bash
bash
```
{% endcode %}



* Exit from a bash instance

{% code overflow="wrap" lineNumbers="true" %}
```bash
exit
```
{% endcode %}



* Change user password

{% code overflow="wrap" lineNumbers="true" %}
```bash
passwd
```
{% endcode %}



* See manual/documentation or found a command

{% code overflow="wrap" lineNumbers="true" %}
```bash
man $command
man -k $keyword        #Make search of command by a keyword
apropos $keyword       #Find a command by description
```
{% endcode %}



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
ls -1        #List each file in a single line
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

* Shows Actual Working directory

{% code overflow="wrap" lineNumbers="true" %}
```bash
pwd
```
{% endcode %}



* Change directory to the specified path

{% code overflow="wrap" lineNumbers="true" %}
```bash
cd        #Redirect to the home directory
cd ~      #Redirect to the home directory
cd $path  #Redirect to the specified file
cd ../    #Redirect to the upper directory
```
{% endcode %}



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



* Update `locate.db` manually

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo updatedb
```
{% endcode %}



* List sockets statistics

{% code overflow="wrap" lineNumbers="true" %}
```bash
ss
```
{% endcode %}



* Create an enviroment variable

{% code overflow="wrap" lineNumbers="true" %}
```bash
$variablename=$value          #Created only in the current shell
export $variablename=$value   #Created globally
```
{% endcode %}



* List enviroment variables

{% code overflow="wrap" lineNumbers="true" %}
```bash
env
```
{% endcode %}



* List command history

{% code overflow="wrap" lineNumbers="true" %}
```bash
history
export HISTCONTROL=$value          #Set output format for history
export HISTIGNORE='$regex'         #Set ignore values for history
export HISTTIMEFORMAT='$options'   #Set time format for history
```
{% endcode %}



* Repeat a command based on hostory

{% code overflow="wrap" lineNumbers="true" %}
```bash
!$number   #Repeat the command with that number
!!         #Repeat last command used
```
{% endcode %}



* Asign a name for simplificated a command or redefine a command

{% code overflow="wrap" lineNumbers="true" %}
```bash
alias $name=$command
alias         #See all defined aliases
unalias       #Delete alias
```
{% endcode %}



* Output any text that we provide

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>echo $text
</strong></code></pre>



* Create a new directory

{% code overflow="wrap" lineNumbers="true" %}
```bash
mkdir $dirname
mkdir ${dirname1,dirname2}            #Create various folders
mkdir -p $dirname/{$subdir1,$subdir2} #Create a folder with subfolders
```
{% endcode %}



* Shows file content in command-line

{% code overflow="wrap" lineNumbers="true" %}
```bash
cat $file
cat $path     #File in the specified file path
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
wc $filename      #Count number of lines, words and characters
wc -l $filename   #Count number of lines
wc -m $filename   #Count number of characters
wc -c $filename   #Count number of bytes
wc -w $filename   #Count number of words
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



* Edit text and streams

{% code overflow="wrap" lineNumbers="true" %}
```bash
sed '$regex' $filename
```
{% endcode %}



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

* Shows the initial or final lines of a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
head $filename #Shows 10 initial lines
head -n$number $filename #Shows the first $number lines
tail $filename #Shows 10 final lines
tail -n$number $filename #Shows the last $number lines
tail -f $filename #Shows appended lines as data grows
```
{% endcode %}



* Execute a command at regular intervals

{% code overflow="wrap" lineNumbers="true" %}
```bash
watch
watch -n$number $command #Execute command every $number seconds
```
{% endcode %}



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

* Download files from the web

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">wget URL
wget -O $name $URL  #Save with a different name
<strong>curl $URL 
</strong><strong>curl -o $name $URL  #Save with a different name
</strong>axel $URL           #Dowload through various connections
axel -n$number $URL #Specify number of connection to use
axel -O $name $URL  #Save with a different name
</code></pre>



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
ps -e     #Shows all processes
ps -f     #Display full format listing
ps -C $commandname  #Shows process with a specified command
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



* Manage packages via Debian

```
dpkg -i $packagename   #Install a package 
dpkg -r $packagename   #Remove a package 
dpkg -P $packagename   #Delete package and its configuration
```



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



* Check NIC configuration

{% code overflow="wrap" lineNumbers="true" %}
```bash
ifconfig     #For all Interfaces
iwconfig     #For wireless Interfaces
```
{% endcode %}
