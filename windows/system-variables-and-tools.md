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

# System Variables and Tools

In Windows, similar to Linux, **environment variables** play a crucial role in influencing how the operating system and its applications behave.&#x20;

They can be accessed through the Command Prompt, PowerShell, and other methods, and can be identified because they start and end with the `%` symbol.

Below we find a list of some of the most usual environment variables:

* **`%WINDIR%`/ `%SystemRoot%`:** Location for the operating system files (`C:\Windows`).
* &#x20;**`%PATH%`**: Specifies directories to search for executable files.
* **`%TEMP%`**: Designates the location where temporary files are stored.
* **`%USERPROFILE%`:** Path to the current user's profile directory, which contains user-specific files and settings (`C:\Users\$username`).
* **`%APPDATA%`:** Path to the application data folder for the current user, used by applications to store user-specific data (`C:\Users\username\AppData\Roaming`).&#x20;
* **`%LOCALAPPDATA%`:** Specifically points to the local application data folder, which is typically used for non-roaming application settings (`C:\Users\username\AppData\Local`).
* **`%PROGRAMFILES%`:** The default installation directory for 32-bit applications on a 64-bit version of Windows (`C:\Program Files`).
* **`%PROGRAMFILES(X86)%`:** The default installation directory for 32-bit applications on a 64-bit version of Windows (usually C:\Program Files (x86)).&#x20;
* **`%SystemDrive%`:** Drive letter where Windows is installed (Usually `C:`).
* **`%COMPUTERNAME%`:** The name of the computer on the network.
* **`%USERNAME%`:** The name of the currently logged-in user.
* **`%DATE%`:** The current system date which is formatted based on the regional settings.
* **`%TIME%`:** The current system time which formatted based on the regional settings.
* **`%NUMBER_OF_PROCESSORS%`:** The number of processors installed on the machine.
* **`%PROCESSOR_ARCHITECTURE%`:** The architecture of the processor, such as _AMD64_ for 64-bit or _x86_ for 32-bit.
* **`%SESSIONNAME%`:** The name of the current session, useful for differentiating between multiple user sessions.
* **`%PSExecutionPolicyPreference%`:** Specifies the execution policy for PowerShell scripts, which determines the level of trust for running scripts.

Also, Windows provides a variety of system tools that allow users to configure settings, monitor system performance, and manage system resources. Following we find a list of some of them:

* **`msconfig`:** System configuration, related to startup options.
* **`taskmgr`:** Task Manager.
* **`msinfo32`:** System information, view of your hardware, system components, and software environment.
* **`resmon`:** Resource Monitor, shows the process and aggregate CPU, memory, disk, and network usage information.
* **`compmgmt.msc`:** Computer Management.
* **`lusrmgr.msc`:** Information about local users and groups of the device.
* **`control.exe`:** Control Panel.
* **`UserAccountControlSettings.exe`:** Change UAC settings.
* **`regedit/regedt32`:** Registry Editor, a central database used to store information necessary to configure the system for users, applications, and hardware devices.
* **`cmd`:** Command Prompt, execute commands from the console.
* **`control /name Microsoft.WindowsUpdate`:** Access to Windows update.
* **`wf.msc`:** Windows firewall.

All of them can be easily accessed via the _Run_ application (Which can be opened with `Windows+R`).
