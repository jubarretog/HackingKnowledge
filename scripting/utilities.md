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

# Utilities

## <mark style="color:purple;">TTY Sanitization</mark>

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



## <mark style="color:purple;">Corrupt history zsh</mark>

Sometimes when using _zsh_ as shell, the history files get corrupted. To correct this issue we can use the followin commands

{% code overflow="wrap" lineNumbers="true" %}
```bash
cd ~
mv .zsh_history .zsh_history_bad
strings .zsh_history_bad > .zsh_history
fc -R .zsh_history
rm ~/.zsh_history_bad
```
{% endcode %}

***



## <mark style="color:green;">Docker</mark>

* Help to build, share, and run container applications.

### Commands

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install docker-ce docker-ce-cli containerd.io
sudo apt install docker-compose-plugin #Install docker compose
```
{% endcode %}

***

* Commands

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">sudo docker rm $containerID #Delete a container
sudo docker build . #Build image from a dockerfile in the actual folder
<strong>sudo docker image ls #List all installed images
</strong>sudo docker image rm $imageID #Delete a installed image
sudo docker container ls        #List all running containers
sudo docker run $containerID    #Run container using ID
sudo docker run $containerName  #Run container using Name
sudo docker run $containerName --rm #Run container but deleted when done
sudo docker run $containerName -p $hostPort:$containerPort #Specificate run ports
sudo docker container stop $containerID #Stop a running container
sudo docker compose up -d #Use .yml file to run various containers in background
</code></pre>

***

