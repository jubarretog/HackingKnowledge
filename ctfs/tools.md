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

# Tools

## <mark style="color:orange;">TTY Sanizitation</mark>

Executing this commands let us configure a terminal to be interactive an process keybinding as a normal bash. Very useful when we get a external terminal, for example with a reverse shell.

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>tty
</strong>script /dev/null -c bash
ctrl +z
stty raw -echo;fg
<strong>reset
</strong>export TERM=xterm
export SHELL=bash
stty rows 24 columns 126
</code></pre>



## <mark style="color:green;">Openvpn</mark>

* Tool for getting acces to a VPN

### Commands

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo openvpn $ovpnfile
```
{% endcode %}

***



## <mark style="color:orange;">Information Sources</mark>

* **LOLBAS:** Contain scripts, binaries and libraries for developing a Living off the Land attack. [https://lolbas-project.github.io/](https://lolbas-project.github.io/)
* **Hacksplaining:** [https://www.hacksplaining.com/lessons](https://www.hacksplaining.com/lessons)



##
