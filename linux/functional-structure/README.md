# Functional Structure

The _Linux_ operating system is **structured** in a tree-like form and follows the Filesystem Hierarchy Standard (FHS). The main file system folders that compose the structure can be represented in the following diagram:

<figure><img src="../../.gitbook/assets/image (262) (1).png" alt="" width="563"><figcaption><p><a href="https://academy.hackthebox.com/module/18/section/94">https://academy.hackthebox.com/module/18/section/94</a></p></figcaption></figure>

## <mark style="color:blue;">Common Directories</mark>

Some common directories in a _Linux_ filesystem that play key roles in system configuration, file storage, operational functions, and performance are:

* _**`/`**_**:** The root filesystem, where all of the files required to boot Linux are stored
* _**`/etc`**_**:** Store configuration files that are used by the operating system
  * _**`/etc/bash.bashrc`**_**:** Script that contains bash settings
  * _**`/etc/passwd`**_**:** List of all user accounts
  * _**`/etc/issue`**_**:** Usually contains information about the OS
  * _**`/etc/crontab`**_**:** Contains the cron jobs that are executed by the system
  * _**`/etc/shadow`**_**:** Contains encrypted information about credentials
* _**`/var`**_**:** Store data that is frequently accessed or written by services or applications running on the system
  * _**`/var/www/html`**_**:** Default store for the server root folder
* _**`/root`**_**:** Home directory of the root system user
* _**`/tmp`**_**:** Temporary files that store data that is only needed to be accessed once or twice. Once the computer is restarted, the content of this folder is cleared out
* _**`/opt`**_**:** Stands for optional, normally third-party software information
* _**`/bin`**_**:** Basic programs of Unix (binaries)
* _**`/sbin`**_**:** Binary programs for system administration
* _**`/usr`**_**:** Contain users' information
  * _**`/usr/bin`**_**:** Installed packages and applications
  * _**`/usr/share`**_**:** Application support and data files
* _**`/proc`**_**:** Contains information about internal jobs and processes of the system
  * _**`/proc/version`**_**:** Information about OS
* _**`/media`**_**:** Where external devices are mounted
