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

# Functional Structure

_Linux_ operating system is **structured** in a tree-like form and follows the Filesystem Hierarchy Standard (FHS). The main file system folders that compose the structure can be represented in the following diagram:

<figure><img src="../../.gitbook/assets/image (262) (1).png" alt="" width="563"><figcaption><p><a href="https://academy.hackthebox.com/module/18/section/94">https://academy.hackthebox.com/module/18/section/94</a></p></figcaption></figure>

## <mark style="color:blue;">Common Directories</mark>

Some common directories in a _Linux_ filesystem that play key roles in system configuration, file storage, operational functions, and performance are:

* **`/`:** Root filesystem where all of the files required to boot Linux are stored
* **`/etc`:** Store configuration files that are used by the operating system
  * **`/etc/bash.bashrc`:** Script that contains bash settings
  * **`/etc/passwd`:** List of all user accounts
  * **`/etc/issue`:** Usually contains information about the OS
  * **`/etc/crontab`:** Contains the cronjobs that are executed by the system
  * **`/etc/shadow`:** Contains encrypted information about credentials
* **`/var`:** Store data that is frequently accessed or written by services or applications running on the system
  * **`/var/www/html`:** Default store for the server root folder
* **`/root`:** Home directory of the root system user
* **`/tmp`:** Temporary files, store data that is only needed to be accessed once or twice, once the computer is restarted, the content of this folder is cleared out
* **`/opt`:** Stands for optional, normally third-party software information
* **`/bin`:** Basic programs of Unix (binaries)
* **`/sbin`:** Binary programs for system administration
* **`/usr`:** Contain users' information
  * **`/usr/bin`:** Installed packages and applications
  * **`/usr/share`:** Application support and data files
* **`/proc`:** Contains information about internal jobs and processes of the system
  * **`/proc/version`:** Information about OS
* **`/media`:** Where external devices are mounted
