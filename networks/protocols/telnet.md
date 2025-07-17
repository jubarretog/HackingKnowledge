# Telnet

The **Telecommunication Network** protocol allows users to remotely access and control devices over a network, typically using port 23. It was widely used for remote administration of systems before being largely replaced by [SSH](ssh.md) due to security concerns about sending the data in plain text, making it vulnerable to interception.

## <mark style="color:green;">Interaction with the protocol</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install telnet
```
{% endcode %}

***

* Connect using the protocol

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo telnet $ip $port
telnet: \>      #Text based interface
telnet: \> exit #Close connection
```
{% endcode %}

***

* Interact with other protocols

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>#Example
</strong><strong>sudo telnet $ip 80 #We connect to HTTP service
</strong>
#We send a petition
GET / HTTP/1.1
host: telnet      #After finishing, hit enter twice to send
</code></pre>

{% hint style="warning" %}
If the host isn't specified, we will get an error&#x20;
{% endhint %}
