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

# Useful Shell Resources

Here are some useful resources that can help in managing terminal environments and resolving common shell-related issues.

## <mark style="color:orange;">TTY Sanitization</mark>

Executing these commands lets us configure a terminal to be interactive and process keybinding as a normal bash. Very useful when we get an external terminal, for example with a reverse shell.

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>tty
</strong>script /dev/null -c bash
#Use Ctrl+Z
stty raw -echo;fg
<strong>reset
</strong>export TERM=xterm
export SHELL=bash
stty rows 24 columns 126
</code></pre>

## <mark style="color:orange;">Corrupt history of</mark> <mark style="color:orange;"></mark>_<mark style="color:orange;">zsh</mark>_

Sometimes when using _zsh_ for our shell, the history files get corrupted. To correct this issue we can use the following commands

{% code overflow="wrap" lineNumbers="true" %}
```bash
cd ~                                    
mv .zsh_history .zsh_history_bad
strings .zsh_history_bad > .zsh_history
fc -R .zsh_history
rm ~/.zsh_history_bad
```
{% endcode %}
