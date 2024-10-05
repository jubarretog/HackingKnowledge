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

By executing `ls -l` we can see a list of details from a file or directory. The first part represents the permissions associated with the file. It looks like a combination of symbols `-` and letters `d` `r` `c` `w` `s`. These can be understood as follows:

* First indicates the type of file: Not special`-`, directory `d`
* Then, three sections of three letters, each one indicating: `owner`, `group` and `others`
* Each letter indicates the permissions: read `r` write: `w` or execute `x` for the respective section

{% code overflow="wrap" lineNumbers="true" %}
```bash
drw-r--r-x     #Directory, Owner read and write, Groups read and Other read and execute
-rwsr--r-x     #This has SUID permissions
-rw-r-sr-x     #This has SGID permissions
```
{% endcode %}

***

* The permissions can also be represented by adding the numbers in each section where `r=4`,  `w=2` and `x=1`

{% code overflow="wrap" lineNumbers="true" %}
```bash
-rw-r--r-x      #Can be represented as 645
-rwxrwxr--      #Can be represented as 774
```
{% endcode %}

***

## <mark style="color:blue;">**Special permissions**</mark>

We find two classes of special permission known as SUID (Set User ID) and SGID (Set Group ID) that allow to run specific applications as root for certain users or groups without being owners.

* The letter `s` indicates SIUD or SGID permissions.

```bash
//-rw-r--r-s      #The letter s represents the special permission
```

***

Also, we can find an extra permission for directories known as Sticky bit, that ensures that only the owner of the file/directory, or the root user can delete or rename files within the directory.

* The letters `t` represents the Sticky bit but users still have execute permissions.
* If shown capitalized (`T`)  all other users do not have access permissions contents to the folder.

```bash
drw-rw-r-t    #Sticky with execute permissions
drw-rw-r-T    #Sticky with no access permissions
```
