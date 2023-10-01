# General Concepts

* **SAM:** Security Account Management database, stores user passwords.
* **NTFS:** New Technology File System, in case of a failure the file system can automatically repair the folders/files on disk using information stored in a log file.
  * **EFS:** Encrypted File System, provides cryptographic protection of individual files on NTFS file system volumes using a public-key system.
  * **ADS:** Alternate Data Streams, file attribute only found on the NTFS file system
  * **NTHash:** Output of the algorithm used to store passwords on Windows systems in the SAM database and on domain controllers
  * **NetNTLMv2:** String specifically formatted to include the challenge and response
* **FAT16/FAT32:** File Allocation Table, file system typically seen as partitions in USB devices, MicroSD cards.
* **HPFS:** High Performance File System
* **UAC:** User Account Control, controls privileges of a user to run tasks on the system.
* &#x20;**WMI:** Windows Management Instrumentation, is the infrastructure for management data and operations on Windows OS.
* **Environment variables:** Store information about the operating system environment.
* **TPM:** Trusted Platform Module, designed to provide hardware-based, security-related functions. A TPM chip is a secure crypto-processor that is designed to carry out cryptographic operations and make devices tamper-resistent.
* **BitLocker:** Help protect user data ensuring that a computer has not been tampered with while the system was offline.
* **Volume Shadow Copy Service:** Coordinates the required actions to create a consistent shadow copy (system snapshot).
