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

# TTY Sanizitation

Executing this commands let us configure a terminal to be interactive an process keybinding as a normal bash. Very useful when we get a external terminal, for example with a reverse shell.

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>tty
</strong>script /dev/null -c bash
#Use Ctrl+Z
stty raw -echo;fg
<strong>reset
</strong>export TERM=xterm
export SHELL=bash
stty rows 24 columns 126
</code></pre>

