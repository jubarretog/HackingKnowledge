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

# SMTP

**Simple Mail Transfer Protocol** operates in the Application Layer and uses TCP ports 25, and 465/587 for encrypted communication. It is the primary protocol used for sending and relaying email messages across the Internet,  by transferring messages between mail servers and sending client applications. SMTP does not handle email retrieval, so it works alongside IMAP or POP3 for receiving emails.

SMTP follows a client-server model in the following way:

* **SMTP Client:** The system, such as an email application or mail transfer agent, sends emails to an SMTP server
* **SMTP Server:** The mail server processes, routes, and delivers email messages to the recipient’s mail server

To facilitate email transfer, SMTP uses a series of commands and response**s** between mail servers. Some of them are:

* `HELO`**/**`EHLO`**:** Identifies the sending mail server to the recipient server
* `MAIL FROM`**:** Specifies the sender’s email address
* `STARTTLS`**:** Switch plaintext connection to encrypted connection
* `RCPT TO`**:** Defines the recipient’s email address
* `DATA`**:** Transfers the content of the email
* `RSET`**:** Abort initiated transmission but keep the connection
* `VRFY`**:** Check if a mailbox is available for message transfer
* `QUIT`**:** Ends the session

SMTP servers also use authentication and encryption mechanisms, such as SSL or TLS to secure email communication.

## <mark style="color:green;">Interaction with protocol</mark>

* Connect to an SMTP server using the [_Telnet_](telnet.md) protocol

{% code overflow="wrap" lineNumbers="true" %}
```bash
telnet $IP 25

# A message like this will be shown
Trying $IP...
Connected to $IP.
Escape character is '^]'.
220 $servername #220 code indicates the connection with the server was successful

#Now is possible to interact with the server
HELO $domain  #Start connection 
```
{% endcode %}

***

* Check for existing users

{% code overflow="wrap" lineNumbers="true" %}
```bash
VRFY $username
252 2.0.0 $username #If exists, we get back a 252 code
```
{% endcode %}

***

* Set sender and receiver

{% code overflow="wrap" lineNumbers="true" %}
```bash
MAIL FROM: <$SenderEmailAddres>
250 2.1.0 Ok   #This is the response of a successful action

RCPT TO: <$ReceiverEmailAddres> NOTIFY=success,failure
250 2.1.5 Ok
```
{% endcode %}

***

* Send data

{% code overflow="wrap" lineNumbers="true" %}
```bash
DATA
354 End data with <CR><LF>.<CR><LF>
$line1
$line2
...
.    #When finished the . defines the end of the message

250 2.0.0 Ok: queued as 6E1CF1681AB #Succesful response will look like this
```
{% endcode %}

***

* Close connection

{% code overflow="wrap" lineNumbers="true" %}
```bash
QUIT
221 2.0.0 Bye
Connection closed by foreign host.
```
{% endcode %}
