# SMB

**Server Message Block** is a network file-sharing protocol that allows applications and users to access files, printers, and other resources on a remote server as if they were local. It operates in the Application layer on ports 445 and 139 and is widely used in _Windows_ networks.

It is commonly used for:

* Centralized storage and file access
* Printer Sharing over the same network
* Domain communication, critical for Active Directory (AD) authentication
* Resource management across a network

The SMB protocol can be accessed from _Linux_ using the [_smbclient_](../tools-and-utilities.md#smbclient) tool, among others.
