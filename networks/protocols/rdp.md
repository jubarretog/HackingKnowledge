# RDP

**Remote Desktop Protocol** is a proprietary protocol developed by _Microsoft_ that allows users to remotely access and control a _Windows_ system over a network connection. It operates in the Application layer on port 3389 and optionally on UDP port 3389 for better performance.

The key Features of RDP are:

* Enables users to control a _Windows_ machine from another device
* Has a GUI unlike [SSH](ssh.md), which is command-line-based
* Allows users to copy/paste text, files, and folders between local and remote systems
* Allows multiple concurrent users in _Windows Server_ editions
* Redirects printers, audio, and other peripherals from the client machine
* Uses TLS encryption and Network Level Authentication (NLA) for security

The RDP protocol can be accessed from _Linux_ using the [_xfreerdp_](../tools-and-utilities.md#xfreerdp) tool, among others.
