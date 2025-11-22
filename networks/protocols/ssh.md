# SSH

**Secure Shell** is a cryptographic network protocol used for secure remote administration of systems over an unencrypted network. It provides encrypted communication between a client and a server, ensuring confidentiality, integrity, and authentication. SSH operates in the Application layer by default on port 22.

This protocol allows users to remotely execute commands on a server, secure file transfer, port forwarding, tunneling, and cryptographic authentication.

## <mark style="color:green;">Interaction with the protocol</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install openssh-client
```
{% endcode %}

***

* Connect using the protocol

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>ssh $user@$IP
</strong><strong>ssh $user@$IP -i $privatekey   #Connect with a private key
</strong>ssh $user@$IP -T               #Connect trying tunneling
scp $file $user@$IP:/tmp/$file #Use SSH for transferring files
</code></pre>
