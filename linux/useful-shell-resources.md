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

Executing these commands lets us configure an interactive terminal and process keybinding like a normal bash. It is very useful when we get an external terminal, for example with a reverse shell.

First, we found the scenario when a connection through SSH is not completely sanitized:

{% code overflow="wrap" lineNumbers="true" %}
```bash
#For setting the terminal colors
export TERM=xterm-256color
source  /etc/skel/.bashrc
#If the last does not work, try with the following
export PS1="\[\e[32m\]\u@\h:\[\e[0m\]\w\$ "

#For setting the proper size
stty size #This is on our local machine to know the number of rows and columns
stty rows $rows columns $columns #This is on the SSH connection with the row and column values of our machine
```
{% endcode %}

Also, we can face the scenario where we have gained a reverse shell to another machine:

{% code overflow="wrap" lineNumbers="true" %}
```bash
#For obtaining a bash
script /dev/null -c bash
#If the last does not work, try with the following
python -c 'import pty;pty.spawn("/bin/bash")'

#For fixing the keybinding
^Z #This refers to making CTRL+Z. It will send the process to the background
stty raw -echo; fg
reset xterm #In some occasions this will not be visible but still write it
export SHELL=bash #To ensure the commands will be interpreted correctly

#For setting the terminal colors
export TERM=xterm-256color
source  /etc/skel/.bashrc
#If the last does not work, try with the following
export PS1="\[\e[32m\]\u@\h:\[\e[0m\]\w\$ "

#For setting the proper size
stty size #This is on our local machine to know the number of rows and columns
stty rows $rows columns $columns #This is on the remote connection with the row and column values of our machine
```
{% endcode %}

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
