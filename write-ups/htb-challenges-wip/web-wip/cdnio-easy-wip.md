---
layout:
  width: default
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
  metadata:
    visible: true
---

# CDNio (Easy) WIP

<figure><img src="../../../.gitbook/assets/image (923).png" alt=""><figcaption></figcaption></figure>

## Description

Race against time! Tweak CDN and caching magic to make web pages load at lightning speed. Minimize cache misses and watch your load times drop!

* **Difficult** <mark style="color:green;">**->**</mark> Easy
* **State** <mark style="color:green;">-></mark> Active

## Summary

* An application with a profile page that fetches information from the logged-in user
* The app has a bot with admin privileges that caches indicated pages via the _/visit_ route
* Cache Deception attack on the _/profile_ route via the Bot´s privileges
* Accessing the profile of the _admin_ user returns the flag in the API-Key field

## Writeup

