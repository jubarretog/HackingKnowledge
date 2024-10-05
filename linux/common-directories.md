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

# Common Directories

Linux OS is structured in a tree-like form and follows the Filesystem Hierarchy Standard (FHS). Below we find a diagram with the structure of the main file system folders:

<figure><img src="../.gitbook/assets/image (262).png" alt=""><figcaption><p><a href="https://academy.hackthebox.com/module/18/section/94">https://academy.hackthebox.com/module/18/section/94</a></p></figcaption></figure>

* **`/`:** Root filesystem where all of the files required to boot Linux are stored.
* **`/etc`:** Store configuration files that are used by the operating system.
  * **`/etc/bash.bashrc`:** Script that contains bash settings.
  * **`/etc/passwd`:** List of all user accounts.
  * **`/etc/issue`:** Usually contains information about the OS.
  * **`/etc/crontab`:** Contains the cronjobs that are executed by the system.
  * **`/etc/shadow`:** Contains encrypted information about credentials.
* **`/var`:** Store data that is frequently accessed or written by services or applications running on the system.
  * **`/var/www/html`:** Default store for the server root folder.
* **`/root`:** Home directory of the root system user.
* **`/tmp`:** Temporary files, store data that is only needed to be accessed once or twice, once the computer is restarted, the content of this folder is cleared out.
* **`/opt`:** Stands for optional, normally third-party software information.
* **`/bin`:** Basic programs of Unix (binaries).
* **`/sbin`:** Binary programs for system administration.
* **`/usr`:** Contain users' information.
  * **`/usr/bin`:** Installed packages and applications.
  * **`/usr/share`:** Application support and data files.
* **`/proc`:** Contains information about internal jobs and processes of the system.
  * **`/proc/version`:** Information about OS.
* **`/media`:** Where external devices are mounted.
