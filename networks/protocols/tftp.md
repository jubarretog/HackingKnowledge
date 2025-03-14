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

# TFTP

**Trivial File Transfer Protocol** is a simplified version of [FTP](ftp.md) used for basic file transfers between network devices. It operates in the Application layer over UDP port 69 and lacks authentication, encryption, or any advanced features.

## <mark style="color:green;">Interaction with protocol</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install tftp
```
{% endcode %}

***

* Connect using the protocol

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">tftp $ip
<strong>tftp:\>          #Text based interface
</strong>tftp:\> get $filename               #Download a file
tftp:\> put $filename               #Upload a file
tftp:\> connect $IP                 #Change server
tftp:\> quit                        #Close connection
</code></pre>
