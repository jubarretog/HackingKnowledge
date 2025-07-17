# IMAP

**Internet Message Access Protocol** is an Application Layer protocol for retrieving emails from a mail server like [POP3](pop-3.md). Its main feature is to allow users to access and manage emails on the mail server without downloading them.

IMAP usually works on port 143 and port 993 for encrypted communication via SSL/TLS. The main features it has are:

* Access and management of emails directly on the mail server
* Supports multiple devices accessing the same mailbox
* Helps with searching, flagging, and organizing emails into folders
* Syncs information so server updates reflect on all devices

POP3 uses a series of commands to interact with mail servers. Some of them are:

* `LOGIN`**:** User's login
* `LIST`**:** Lists directories
* `CREATE`**:** Create a mailbox
* `DELETE`**:** Delete a mailbox
* `RENAME`**:** Rename a mailbox
* `SELECT INBOX`**:** Select a mailbox to access its messages
* `UNSELECT`**:** Exits the selected mailbox
* `FETCH`**:** Retrieves data associated with a message in the mailbox
* `CLOSE`**:** Removes all messages with the _Deleted_ flag
* `LOGOUT`**:** Close the connection
