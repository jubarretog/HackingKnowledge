# Get information from SSL certificates

We can check the content and filter information from an SSL certificate of a website using the HTTPS protocol using the `curl` command, by checking the [_crt.sh_](../tools-and-utilities.md#crt.sh) registers for that site

* Get info of the certificate as _JSON_

{% code overflow="wrap" lineNumbers="true" %}
```bash
curl -s https://crt.sh/\?q\=$domain\&output\=json | jq .
```
{% endcode %}

***

* Filter subdomains from the certificate and save them to a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
curl -s https://crt.sh/\?q\=$domain\&output\=json | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u > subdomainlist.txt
curl -s "https://crt.sh/?q=$domain&output=json" | jq -r '.[] | select(.name_value | contains("$subdomain")) | .name_value' | sort -u #Alternative
```
{% endcode %}

***

* Identify the hosts directly accessible from the Internet and not hosted by third-party providers

{% code overflow="wrap" lineNumbers="true" %}
```bash
for i in $(cat subdomainlist.txt);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f1,4;done > hostIPs.txt
```
{% endcode %}

***

* Use [_Shodan_](../tools-and-utilities.md#shodan) to investigate the IP addresses found

{% code overflow="wrap" lineNumbers="true" %}
```bash
for i in $(cat hostIPs.txt | cut -d" " -f2);do shodan host $i;done
```
{% endcode %}
