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

# Enumeration

First step is to do an enumeration of resources of the target machine such as:&#x20;

* Operative System
* Kernel
* Services running
* Available ports
* Sudo permissions
* Normal and hidden files and directories
* Enviroment variables
* Network interfaces and configuration
* Applications and programming languages installed

## <mark style="color:blue;">Useful Tips</mark>

* Use `hostname` and `whoami` commands
* Use `uname -a`
* Make `cat /proc/version` to get more information about OS
* Make `cat /etc/issue` to know OS information
* Make `ps -A` to show running processes on the current shell (`ps axjf` for tree transformation)
* Use `env` to see enviroment variables
* Use `id` to obtain information abot user and groups, or even info of another user
* Use `ls -la` to check hidden files
* Make `cat /etc/passwd | cur -d ":" -f 1` or `cat /etc/passwd | grep "home"` to know existing users&#x20;
* Check last used commands with `history`
* Check network interfaces with `ifconfig` to know if could be a pivoting point to another network. Then use `ip route` to confirm an interface cannot be accesed directly by the machine (it won't say it is a default interface).
* Use `netstat` to obtain information about listening ports and services running
* Search for specific files with `find`
* Use tools such as _linpeas_ or _linenum_

