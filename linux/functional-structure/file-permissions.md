# File Permissions

**File permissions** in _Linux_ determine who can read, write, or execute a file or directory. Understanding these permissions is essential for managing system security and functionality.

By executing the `ls -l` command, a list of details from a file or directory will be displayed. The first part represents the permissions associated with the file. It looks like a combination of symbols `-` and letters `d` `r` `c` `w` `s`. These can be understood as follows:

* First indicates the type of file: Not special (`-`), directory (`d`)
* Then, we find three sections of three letters, each one indicating: _owner_, _group_, and _other_
* Each letter indicates the permissions: read (`r`), write (`w`), or execute (`x`) for the respective section

{% code overflow="wrap" lineNumbers="true" %}
```bash
drw-r--r-x     #Is a Directory, the Owner can read and write, the Group can read, and Other can read and execute
-rwsr--r-x     #This has SUID permissions because it has s on the Owner section
-rw-r-sr-x     #This has SGID permissions because it has s on the Group section
```
{% endcode %}

***

* The permissions can also be represented by adding the numbers in each section, where `r=4`,  `w=2` and `x=1`

{% code overflow="wrap" lineNumbers="true" %}
```bash
-rw-r--r-x      #Can be represented as 645
-rwxrwxr--      #Can be represented as 774
```
{% endcode %}

***

## <mark style="color:blue;">**Special permissions**</mark>

Two classes of special permission, known as SUID (Set User ID) and SGID (Set Group ID), allow running specific applications as the _root_ user for certain users or groups without being the owners.

* The letter `s` indicates SIUD or SGID permissions

```bash
//-rw-r--r-s      #The letter s represents the special permission
```

***

Also, we can find an extra permission for directories known as Sticky bit, which ensures that only the owner of the file/directory, or the root user, can delete or rename files within the directory.

* The letters `t` represents the Sticky bit, but users still have execution permissions
* If shown capitalized (`T`) all other users do not have access permissions to the folder contents

```bash
drw-rw-r-t    #Sticky with execute permissions
drw-rw-r-T    #Sticky with no access permissions
```
