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

# DNS

## <mark style="color:orange;">Domain Hierarchy</mark>

### TLD (Top-Level Domain)

* Is the righthand part of a domain name.&#x20;
* Can only use a-z 0-9 and hyphens and cannot start or end with hyphens or have consecutive hyphens.
* Can be classified in two types:
  * _gTLD:_ Generic Top Level, tell the user the domain name's purpose.
  * _ccTLD:_ Country Code Top Level Domain, used for geographical purposes.&#x20;

### Second-Level Domain

* Most tipical part of the domain that specifies the name of the page.
* Is limited to 63 characters.

### Subdomain

* Describe an specific applications of a page.
* Can use multiple subdomains but length must be kept to 253 characters or less.
* There is no limit to the number of subdomains you can create for a domain name.



## <mark style="color:orange;">Record Types</mark>

* **A Record:** Resolve to IPv4 addresses
* **AAAA Record:** Resolve to IPv6 addresses
* **CNAME Record:** Resolve to another domain name, then Another DNS request would then be made to the second domain to work out the IP address.
* **MX Record:** Resolve to the address of the servers that handle the email for the domain you are querying.&#x20;
  * Comes with a priority flag that tells the client in which order to try the servers.
* **TXT record:** Are free text fields where any text-based data can be stored. Help to list servers that have the authority to send an email on behalf of the domain.
  * Can help in the battle against spam and spoofed email). They&#x20;
  * Can be used to verify ownership of the domain name when signing up for third party services.

