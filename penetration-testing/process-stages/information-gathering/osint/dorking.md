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

# Dorking

It is a practice that consists of using _Google_ tools and advanced search engines to get information. Also known as Google Hacking but can be transpilled to some other search engines.

* Show results only for the address specified

{% code overflow="wrap" lineNumbers="true" %}
```bash
site:$domain
```
{% endcode %}

***

* Show results with the specified word in the URL

{% code overflow="wrap" lineNumbers="true" %}
```bash
inurl:$phrase
```
{% endcode %}

***

* Show results with the specified word in the contents

{% code overflow="wrap" lineNumbers="true" %}
```bash
intext:$phrase
inbody:$phrase #Alternative
```
{% endcode %}

***

* Show results with the specified extension

{% code overflow="wrap" lineNumbers="true" %}
```bash
filetype:$extension
```
{% endcode %}

***

* Show results with the specified word in the title

{% code overflow="wrap" lineNumbers="true" %}
```bash
intitle:$phrase
```
{% endcode %}

***

* Show results with specific links

{% code overflow="wrap" lineNumbers="true" %}
```bash
link:$link
```
{% endcode %}

***

* Search for results with exact matching

{% code overflow="wrap" lineNumbers="true" %}
```bash
$option:"$phrase"
```
{% endcode %}

***

* To exclude an option from the search

{% code overflow="wrap" lineNumbers="true" %}
```bash
-$option:$value
```
{% endcode %}

***

* Logic operators can be used too

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>$option:$value OR $option:$value
</strong>$option:$value AND $option:$value
$option:$value NOT $option:$value
</code></pre>

***

* Use a wildcard for any character or word

{% code overflow="wrap" lineNumbers="true" %}
```wasm
$option:$value*
```
{% endcode %}

## <mark style="color:green;">Google Hacking Database</mark>

* Collection of Google Dorks, which are specially crafted search queries used to find exposed sensitive information on the internet
* It can be found [here](https://www.exploit-db.com/google-hacking-database) and it's provided by [_Exploit DB_](../../exploitation/tools-and-utilities.md#exploit-db)
