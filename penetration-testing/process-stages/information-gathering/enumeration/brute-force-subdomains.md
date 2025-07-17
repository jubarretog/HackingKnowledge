# Brute-force subdomains

Knowing the domain of a site and its DNS server IP, we could brute-force the subdomains to get access to other exposed sites.

* Bruteforce using a dictionary of well-known names

{% code overflow="wrap" lineNumbers="true" %}
```bash
for sub in $(cat /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt);do dig $sub.<Domain> @<DNSip> | grep -v ';\|SOA' | sed -r '/^\s*$/d' | grep $sub | tee -a subdomains.txt;done
```
{% endcode %}

{% hint style="info" %}
We have to set the _Domain_ and _DNSip_ values, and the result will be saved in _subdomains.txt_
{% endhint %}

***

* Use the _dnsenum_ tool to brute force the subdomains

{% code overflow="wrap" lineNumbers="true" %}
```bash
dnsenum --dnsserver $DNSip --enum -p 0 -s 0 -o subdomains.txt -f /usr/share/SecLists/Discovery/DNS/subdomains-top1million-110000.txt $domain
```
{% endcode %}
