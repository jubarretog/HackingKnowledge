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

# POP 3

**Post Office Protocol version 3** is an Application Layer protocol for retrieving emails from a mail server like IMAP. While [SMTP](smtp.md) is used for sending emails, these protocols handle receiving and managing them on client devices.

POP3 works on Ports 110  and port 995 for encrypted communication via SSL/TLS. The main features it has are:

* Downloads emails from the server to the client’s device
* Best for single-device email access
* Once emails are downloaded, they are typically removed from the server
* Simpler than IMAP and requires less storage on the mail server

POP3 uses a series of commands to interact with mail servers. Some of them are:

* `USER`**:** Identify a user
* `PASS`**:** Authenticate using password
* `STAT`**:** Request the number of emails on the server
* `LIST`**:** Request the number and size of all emails
* `RETR`**:** Request to show an email by ID
* `DELE`**:** Request to delete an email by ID
* `CAPA`**:** Request to display the server capabilities
* `RSET`**:** Request to reset the transmitted information
* `QUIT`**:** Close the connection
