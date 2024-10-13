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

# OSINT

Open Source Intelligence, is the process of collecting public information and analyzing data to relate it and transform it into useful knowledge.

Between the techniques related to OSINT, we can find advanced control of search engines, social media profiling, metadata extraction, leaked data, breached databases, and email harvesting, among others.

Here are some techniques for OSINT purposes:

## <mark style="color:orange;">Dorking</mark>

Also known as Google Hacking, it is a practice that consists of using Google tools and advanced search engines to get information

### Example of use

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

* To exclude an option from the search

{% code overflow="wrap" lineNumbers="true" %}
```url
-$option:$value
```
{% endcode %}
