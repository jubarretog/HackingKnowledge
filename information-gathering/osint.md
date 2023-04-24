# OSINT

Open Source Intelligence, practice based on collecting info from open source sites on the web

## Dorking

Prectice that consist in using google tools and advance serch engine to get information

* Show results only for the adress specified

{% code overflow="wrap" lineNumbers="true" %}
```url
site:$Domain
```
{% endcode %}



* Show results with the specified word in url

{% code overflow="wrap" lineNumbers="true" %}
```url
inurl:$word
```
{% endcode %}



* Show results with the specified extension

{% code overflow="wrap" lineNumbers="true" %}
```url
filetype:$extension
```
{% endcode %}



* Show results with the specified word in title

{% code overflow="wrap" lineNumbers="true" %}
```url
intitle:$word
```
{% endcode %}



* To exclude a option from search

{% code overflow="wrap" lineNumbers="true" %}
```url
-$option:$value
```
{% endcode %}
