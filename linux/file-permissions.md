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

# File Permissions

By executing `ls -l` we can see a list of details from a file or directory. The first part represent the permissions associates with the file. It looks as a combination of symbol `-` and letters `d` `r` `c` `w` `s` and can be understood as following:

* First indicates type of file: Not special`-`, directory `d`
* Then, three sections of three letters, each one indicates: `owner`, `group` and `others`
* Each letter indicates the permissions: read `r` write: `w` or execute `x` for the respective section
* The letter `s` indicates SIUD or SGID permissions.

## <mark style="color:blue;">**Example**</mark>

{% code overflow="wrap" lineNumbers="true" %}
```bash
drw-r--r-x     #Directory, Owner read and write, Groups read and Other read and execute
-rwsr--r-x     #This has SUID permissions
-rw-r-sr-x     #This has SGID permissions
```
{% endcode %}

***

* The permission can also be represented by adding the numbers in each section where `r=4`,  `w=2` and `x=1`

{% code overflow="wrap" lineNumbers="true" %}
```bash
-rw-r--r-x      #Can be represented as 645
-rwxrwxr--      #Can be represented as 774
```
{% endcode %}

***

