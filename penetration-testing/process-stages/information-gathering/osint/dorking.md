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

Also known as Google Hacking, it is a practice that consists of using _Google_ tools and advanced search engines to get information

* Show results only for the address specified

{% code overflow="wrap" lineNumbers="true" %}
```url
site:$Domain
```
{% endcode %}

***

* Show results with the specified word in the URL

{% code overflow="wrap" lineNumbers="true" %}
```url
inurl:$word
```
{% endcode %}

***

* Show results with the specified extension

{% code overflow="wrap" lineNumbers="true" %}
```url
filetype:$extension
```
{% endcode %}

***

* Show results with the specified word in the title

{% code overflow="wrap" lineNumbers="true" %}
```url
intitle:$word
```
{% endcode %}

***

* Show results with referenced hyperlinks

{% code overflow="wrap" lineNumbers="true" %}
```url
Link:$word
```
{% endcode %}

***

* To exclude an option from the search

{% code overflow="wrap" lineNumbers="true" %}
```url
-$option:$value
```
{% endcode %}

***

* Logic operators can be used too

<pre data-overflow="wrap" data-line-numbers><code><strong>$option:$value OR $option:$value
</strong></code></pre>
