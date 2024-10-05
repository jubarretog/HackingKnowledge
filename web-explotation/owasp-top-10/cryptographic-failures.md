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

# Cryptographic Failures

Any misuse or lack of cryptographic security. Most common examples are weak password hashing, use of http instead of https, vulnerable javascript web tokens.

### Example:

* Assume we have got a password hash

{% code overflow="wrap" lineNumbers="true" %}
```bash
#Save password in a file 
echo $hash > $file.hash

#Break the hash
hashcat -a $attackmode -m $hashtype $hashFile $dictionary
#Example
hashcat -a 0 -m 400 password.hash ~/Seclist #400 for php, 0 straight
```
{% endcode %}

***

