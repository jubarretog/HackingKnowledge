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

# Retrieve information from IMAP/POP3 servers

We can interact with IMAP and POP3 mail servers to retrieve information and messages from them, using the `curl` command. Also, we can interact with the encrypted channels for those services as well by using the OpenSSL tool.

* Interact with IMAP server

{% code overflow="wrap" lineNumbers="true" %}
```bash
curl -k 'imaps://$IP' --user $user:$password -v
```
{% endcode %}

***

* Encrypted interaction with POP3

{% code overflow="wrap" lineNumbers="true" %}
```bash
openssl s_client -connect $IP:pop3s

#Once connected we can use the protocol commands
USER $username #Set user
PASS $password #Set password and log in
LIST  #List mails available
RETR $index #Get the content of an email
DELE $index #Delete an email from the server
RSET #Reset deletion marks
QUIT #Close connection
```
{% endcode %}

***

* Encrypted interaction with IMAP

{% code overflow="wrap" lineNumbers="true" %}
```bash
openssl s_client -connect $IP:imaps

#Once connected we can use the protocol commands
A001 LOGIN $username $password    #Log in to server
A002 LIST "" "*" #List all elements in the server
A003 SELECT $servername #Select a mail server to interact with
A005 FETCH $index BODY[] #Get the content of an email
EXPUNGE #Delete or marked emails
QUIT #Close connection
```
{% endcode %}
