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

# Explotation

After enumeration comes the explotation phase were we use vulnerabilities found and CVEs asociated to the target for getting a higher privilege account on the system.&#x20;

Explotation can also set as objective to jump to another machine in the same network via pivoting or even jump to another network.

## <mark style="color:blue;">Useful Tips</mark>

* Run _calc.exe_ on windows as a PoC that we can run commands.
* On metasploit check _Rank_ column of an exploit to ensure its reliability.
* Check kernel version to find any posible exploit
* Use `sudo -l`  to check sudo execution permissions and environment options
* Check executable with _SUID_ or _SGID_ permissions.
* Check wich binaries have capabilities assigned
* Check which cronjobs are programmed to be executed
* Check cronjobs that may be deleted from system but no from _crontab_
* Check writables folders that can be vulneable to abusing of _PATH_ enviroment variable
* Check NFS configuration files to create a conection with the host machine

