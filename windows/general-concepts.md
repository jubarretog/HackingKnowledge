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

# General Concepts

* **SAM:** Security Account Management database, stores user passwords.
* **NTFS:** New Technology File System, in case of a failure the file system can automatically repair the folders/files on disk using information stored in a log file.
  * **EFS:** Encrypted File System, provides cryptographic protection of individual files on NTFS file system volumes using a public-key system.
  * **ADS:** Alternate Data Streams, file attribute only found on the NTFS file system.
  * **NTHash:** Output of the algorithm used to store passwords on Windows systems in the SAM database and on domain controllers.
  * **NetNTLMv2:** String specifically formatted to include the challenge and response.
* **FAT16/FAT32:** File Allocation Table, file system typically seen as partitions in USB devices, MicroSD cards.
* **HPFS:** High-Performance File System.
* **UAC:** User Account Control, controls privileges of a user to run tasks on the system. Even an administrator user has to get verification through it to run a process with root privileges.
* &#x20;**WMI:** Windows Management Instrumentation, is the infrastructure for management data and operations on Windows OS.
* **Environment variables:** Store information about the operating system environment.
* **TPM:** Trusted Platform Module, designed to provide hardware-based, security-related functions. A TPM chip is a secure crypto-processor that is designed to carry out cryptographic operations and make devices tamper-resistant.
* **BitLocker:** Help protect user data ensuring that a computer has not been tampered with while the system was offline.
* **Volume Shadow Copy Service:** Coordinates the required actions to create a consistent shadow copy (system snapshot).
* **`/WINDOWS/system32/drivers/etc/hosts`:** Common file to save hostnames and IPs in Windows.
* **Command Prompt:** A command-line interpreter that allows users to execute commands from a text-based interface. It supports a wide range of commands for file manipulation, system configuration, and troubleshooting.
* **Powershell:** A command-line interpreter that supports a wide range of commands for automating administrative tasks, managing complex configurations, and interacting with web services or APIs. It integrates the .NET framework and offers advanced scripting capabilities.
