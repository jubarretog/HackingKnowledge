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

As _Linux_ is a command-line-based operating system, the use of **commands** is crucial for interacting with the system, performing tasks, and managing files and applications.&#x20;

Here is a list of essential and useful commands:

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

* See the manual/documentation or find a command

{% code overflow="wrap" lineNumbers="true" %}
```bash
man $command
man -k $keyword        #Make a search of command by a keyword
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

* Get information about users logged in

{% code overflow="wrap" lineNumbers="true" %}
```bash
whoami #Shows the currently logged-in user
who    #Shows all logged-in users
```
{% endcode %}

***

* Get the name of the computer

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
uname -r #Print kernel version
uname -m #Print machine hardware name
```
{% endcode %}

{% hint style="info" %}
Information comes in the following order separated by spaces:

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

* Executes a command with superuser permissions

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

* List files, directories, devices, and more

{% code overflow="wrap" lineNumbers="true" %}
```bash
ls           #In the actual directory
ls $path     #In path directory
ls -a        #Include hidden files
ls -1        #List each file in a single line
ls -l        #File permissions, associated user and groups, creation date and hour
ls -l -lr    #List and order in z-a order
ls -l -lt    #List and order by last modified
ls -i        #List with index/inode number
lsof         #List open files
lsusb        #List USB devices
lsblk        #List disk partitions
```
{% endcode %}

{% hint style="info" %}
Hidden files start with a dot, for example _.hiddenfile_
{% endhint %}

***

* Change permissions of a file

```bash
sudo chmod +$permision $filename      #Add permission
sudo chmod -$permision $filename      #Remove permission
sudo chmod -R 777 $filename           #Give all permission to everyone
sudo chown $owner:$group $filename    #Change owner and group of a file
```

***

* Shows Actual Working directory

{% code overflow="wrap" lineNumbers="true" %}
```bash
pwd
```
{% endcode %}

***

* Change the directory to the specified path

{% code overflow="wrap" lineNumbers="true" %}
```bash
cd        #Redirect to the home directory
cd ~      #Redirect to the home directory
cd $path  #Redirect to the specified file
cd ../    #Redirect to the upper directory
cd -      #Redirect to the last directory
```
{% endcode %}

***

* Get the path of the file by searching in directories defined at the `$PATH` environment variable

{% code overflow="wrap" lineNumbers="true" %}
```bash
which $filename
```
{% endcode %}

***

* Get the path of a file by searching in _locate.db_

{% code overflow="wrap" lineNumbers="true" %}
```bash
locate $filename
sudo updatedb    #Update locate.db
```
{% endcode %}

{% hint style="info" %}
_locate.db_ is a built-in database of system files
{% endhint %}

***

* Update _locate.db_ manually

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo updatedb
```
{% endcode %}

***

* List sockets/services statistics

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

* Repeat a command based on the history

{% code overflow="wrap" lineNumbers="true" %}
```bash
!$number   #Repeat the command with that number
!!         #Repeat the last command used
```
{% endcode %}

***

* Open a file, usually graphic files such as images and PDFs

{% code overflow="wrap" lineNumbers="true" %}
```bash
open $filename
display $imagefile
```
{% endcode %}

***

* Assign a name for simplified a command or redefine a command

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
more $file #Charge one page of content at the time
less $file #Same as more but have more features
```
{% endcode %}

***

* Find a file or directory

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>find .                      #All files and directories from the actual directory
</strong>find /                      #All files and directories from root directory
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
find . -atime $n            #Files accessed in the last n days
<strong>find . -cmin $n             #Files changed in the last n minutes
</strong>find . -amin $n             #Files accessed in the last n minutes
find . -newermt $date       #Files newer than the specified date
find . 2>/dev/null          #Exclude files with standard errors
</code></pre>

{% hint style="info" %}
The `-perm`option can receive permission such as `777` or `a=x`
{% endhint %}

***

* Count the number of entries in a file or output

{% code overflow="wrap" lineNumbers="true" %}
```bash
wc $filename      #Count the number of lines, words, and bytes
wc -l $filename   #Count number of lines
wc -m $filename   #Count number of characters
wc -c $filename   #Count number of bytes
wc -w $filename   #Count number of words
wc $filename $filename #Count various files and show the total for each one
```
{% endcode %}

***

* Search through a file and show any entries with the specified value

{% code overflow="wrap" lineNumbers="true" %}
```bash
grep "$text" $filename
grep -i "$text" $filename   #Ignore the value given
grep -v "$text" $filename   #Returns non-matching results
grep -e "$ReGex" $filename  #Use regular expressions
egrep "$ReGex" $filename    #Alternative for use of regular expressions
```
{% endcode %}

{% hint style="info" %}
Remembering the use of RegEx:

* (a) -> Close and expression
* \[a-z] -> Indicates a class of characters (In this case letters)
* {1,10} -> Indicates how many times a pattern must be repeated (In this case 1 to 10 times)
* \| -> Works as the _OR_ logical operator
* .\* -> Works as the _AND_ logical operator
{% endhint %}

***

* Edit text and streams on output

{% code overflow="wrap" lineNumbers="true" %}
```bash
sed 's/$objetive/$replacement/g' $filename
```
{% endcode %}

***

* Extract a section of text from the file

{% code overflow="wrap" lineNumbers="true" %}
```bash
cut -f $fieldnumber -d "$delimiter" $filename
awk '{print $field, $field}' #By default space as separator, fields are columns
awk '{print $1, $NF}' #With $1 get first line result, with $NF last line result
awk -F "$delimiter" '{print $field, $field}' #Spicify delimiter
```
{% endcode %}

***

* Sort lines of a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
sort $filename     #Order by alphabet using the first character
sort -f $filename  #Ignore Case sensitive
sort -u $filename  #Count and not repeat if the same
sort -r $filename  #Reverse the result
sort -n $filename  #Compare as numerical value
sort -k $field$delimitertor$position $filename #Order by field and position
```
{% endcode %}

***

* Find unique occurrences in a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
sort $filename | uniq 
sort $filename | uniq -c #Count number of occurrences
sort $filename | uniq -b #Get repeated lines
```
{% endcode %}

{% hint style="info" %}
`uniq` needs a sort file as input to work correctly
{% endhint %}

***

* Compare the content of files

{% code overflow="wrap" lineNumbers="true" %}
```bash
comm $file1 $file2
comm -$number $file1 $file2  #Supress specified lines
diff $file1 $file2 
diff -c $file1 $file2     #Ouput in context format
diff -u $file1 $file2     #Ouput in unified format
```
{% endcode %}

{% hint style="info" %}
In `comm` output first the columns. Represents unique lines for the first file, the second column the unique lines for the second file, and the third column the lines both share
{% endhint %}

***

* Shows the content of a file with replacements on the output

{% code overflow="wrap" lineNumbers="true" %}
```bash
tr $filename $expression $replacement
tr $filename -c $expression $replacement #What not match is replaced
tr $filename -d $expression #Delete what coincides with expression
```
{% endcode %}

***

* Format the output in columns

{% code overflow="wrap" lineNumbers="true" %}
```bash
column $file -t         #By default use space as a separator
column $file -t -s $sep #Use set of characters as separator
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

* Transform hex dump

{% code overflow="wrap" lineNumbers="true" %}
```bash
xdd $filename        #Show hex dump of the file
xdd -r $filename     #Reverse hex dump to a file
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

* Shows the type of file

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

* Create or edit a file through the command line

{% code overflow="wrap" lineNumbers="true" %}
```bash
nano $filename
nano -B $filename #Make a backup when opening a file with nano
vi $filename      #More powerful Text Editor
vim $filename     #Improved version of vi
vimtutor          #Enter tutor mode for practicing
```
{% endcode %}

{% hint style="info" %}
In Unix the `^` symbol represents the _Ctrl_ key
{% endhint %}

***

* Shows estimated disk usage of a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
du $filename
du -h $filename    #Shows output in human-readable mode
du -b $filename    #Shows output in bytes mode
```
{% endcode %}

***

* Make petitions to websites

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>curl $URL                          #Make a get petition
</strong>curl -L $URL                       #Follow redirections
curl -O $URL/$file                 #Save a file with the same name
<strong>curl -o $name $URL/$file           #Save a file with a different name
</strong>curl -o $URL/$file1 -o $URL/$file2 #Get various files
curl $URL -d "$param=$value"       #Specificate values of body
curl -X $PETITION $URL             #Make an specific type of petition
curl $firstpetition --next $secondpetition #Make various petition
curl $URL -H "$header:$value"      #Specific header in a petition
curl $URL -v                       #Get verbose output
curl -IL $URL                      #Catch header, useful for banner grabbing
wget $URL
wget -O $URL/file          #Save a file with the same name
wget -o $name $URL/file    #Save a file with a different name
axel $URL                  #Dowload through various connections
axel -n$number $URL        #Specify the number of connections to use
axel -O $name $URL         #Save with a different name
</code></pre>

***

* Verify MD5 encryption for a file

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
ps                  #Show process run in the user session
ps aux              #Shows other user and complete system processes
ps -A               #Shows all processes
ps -f               #Display full format listing
ps -C $commandname  #Shows process with a specified command
ps axjf             #Show as a tree
top                 #Real-time information about the system running processes
```
{% endcode %}

***

* Kill a system process, we can send some signals to specify the type of killing

{% code overflow="wrap" lineNumbers="true" %}
```bash
kill -9 $PID
kill -s SIGTERM $PID   #Kill the process, but allow  to do some cleanup
kill -s SIGKILL $PID   #Kill the process but doesn't do any cleanup
kill -s SIGSTOP $PID   #Stop/suspend a process
kill -s SIGINT $PID    #Interrupt a process (same as CTRL+C)
kill -s SIGQUIT $PID   #Quit process (same as CTRL+D)
kill -s SIGTSTP $PID   #Suspend process but can still be handled (same as CTRL+Z)
kill -l                #See all possible signals that can be sent
```
{% endcode %}

{% hint style="info" %}
The process with a PID equal to 0 is a process that starts when the system boots
{% endhint %}

***

* Manage system processes and services

{% code overflow="wrap" lineNumbers="true" %}
```bash
systemctl $option $process
systemctl start $process       #For starting a process
systemctl stop $process        #For killing a process
systemctl enable $process      #Set process to start at startup
systemctl disable $process     #Set process to not start at startup
systemctl status $Process      #View the status of a process
systemctl list-unit-files      #List the status of all processes
systemctl list-units --type=service #List status of all services
journalctl -u $service --no-pager #See logs of a service
```
{% endcode %}

***

* Handle background processes

{% code overflow="wrap" lineNumbers="true" %}
```bash
jobs          #List all actual background processes
bg            #Resume stopped background processes
bg $PID       #Send specified process to background
fg $PID       #Foreground a background process
fg %$jobID    #Foreground specified list ID process
fg %$String   #Refers to the beginning of the suspended process
fg %+         #Refers to the current job
fg %-         #Refers to the previous job
```
{% endcode %}

{% hint style="info" %}
`bg` can only be used after stopping a process with `^z`
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
Every user has only one crontab
{% endhint %}

***

* Manage packages, repositories, and digital signatures from APT

{% code overflow="wrap" lineNumbers="true" %}
```bash
apt install $packagename   #Install a package
apt reinstall $packagename #Reinstall a package from scratch
apt remove $packagename    #Remove a package
apt remove --purge $packagename  #Delete package and its configuration
apt update $packagename    #Update a package
apt update                 #Update all packages
apt upgrade                #Update Linux system and applications
apt-get                    #Use the first version for actions
apt-cache search $toolname #Search for a tool in apt repositories
apt show $packagename      #Show information about a package
add-apt-repository         #Add repositories from developers to your apt lists
apt-key add $filename      #Add key file to trusted keys list
apt-key del $keyID         #Remove key trusted keys list
apt-key list               #List all trusted keys
apt list --installed | grep "installed" | wc -l #Check number of installed packages

```
{% endcode %}

***

* Manage packages via Debian

```bash
dpkg -i $packagename   #Install a package
dpkg -r $packagename   #Remove a package 
dpkg -P $packagename   #Delete package and its configuration
```

***

* Test if the connection to a remote resource is possible

{% code overflow="wrap" lineNumbers="true" %}
```bash
ping $IPaddress
ping $URLdomain                 #Use domain name
ping $IPaddress -4              #Limit to only IPv4 requests
ping $IPaddress -6              #Limit to only IPv6 requests
ping $IPaddress -i $seconds     #Set time interval to send each packet
ping $IPaddress -v              #Show a verbose output
ping $IPaddress -c $number      #Send an exact number of packet
ping $IPaddress -s $size        #Specify the number of bytes of the data
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
A `*` symbol on the response represents that a package hasn't received an ICMP message from the router.
{% endhint %}

***

* Gather information about with DNS lookups

{% code overflow="wrap" lineNumbers="true" %}
```bash
whois $URLdomain     #Get domain register information
host 72.163.10.1     #Do reserve lookup to get a host names
```
{% endcode %}

***

* Obtain IP and record information from a domain

{% code overflow="wrap" lineNumbers="true" %}
```bash
nslookup $URLdomain
nslookup $URLdomain $serverIP #Change server used to perform lookups
nslookup -type=$record $URLdomain    #Specify record type

nslookup #Enter interactive mode
> Exit   #Quit interactive mode
```
{% endcode %}

***

* Query recursive DNS servers for domain's information

{% code overflow="wrap" lineNumbers="true" %}
```bash
dig $URLdomain $record
dig $URLdomain $serverIP #Change server used to perform lookups
dig @$DNSIPaddress $URLdomain           #Look up DNS records
dig @$DNSIPaddress $URLdomain $record   #Specify record type on DNS records
dig -x $IP             #Perform reverse DNS lookups
```
{% endcode %}

***

* Manage disk partition table

{% code overflow="wrap" lineNumbers="true" %}
```bash
fdisk $device
fdisk -l       #List all current disk partitions
```
{% endcode %}

***

* Network Utilities

{% code overflow="wrap" lineNumbers="true" %}
```bash
ifconfig     #Check network interfaces
ifconfig $interface up #Activate a network interface
ifconfig $interface $IP #Assign IP Address to an Interface
ifconfig $interface netmask $mask #Assign a Netmask to an Interface
route add default gw $IP $interface
iwconfig     #Check only wireless Interfaces
ip route     #Check existing network routes
ip link set $interface up #Activate a network interface
netstat      #Check ports and active connections
netstat -a   #List all ports and connection
netstat -l   #List listening ports
netstat -t   #List only TCP ports
netstat -u   #List only UDP ports
netstat -s   #List network usage statistics by protocol
netstat -p   #List with PID and program name
netstat -ano #Most common use, n to no resolve names, o to display timers
```
{% endcode %}

{% hint style="info" %}
When using `netstat -p` if the PID and name aren't shown, it's because the process is owned by another user. Running the command with `sudo` could show this information
{% endhint %}

***

* List capabilities of all binary files

{% code overflow="wrap" lineNumbers="true" %}
```bash
getcap -r / 2>/dev/null #Is good practice to redirect errors if not run with sudo
```
{% endcode %}

***

* Modify users, groups and passwords

{% code overflow="wrap" lineNumbers="true" %}
```bash
useradd    #Creates a new user or update default new user information
userdel    #Deletes a user account and related files
usermod    #Modifies a user account
addgroup   #Adds a group to the system
delgroup   #Deletes a group of the system
passwd     #Changes user password
```
{% endcode %}
