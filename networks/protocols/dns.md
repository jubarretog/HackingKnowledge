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

The DNS (Domain Name System) protocol is a critical part of how the internet functions. It acts like a phonebook for the internet by translating human-friendly domain names into IP addresses.

For example, when users enter a domain name in their browser (_google.com_), the DNS queries multiple servers to resolve the name into the corresponding IP address (_8.8.8.8_).

## <mark style="color:blue;">Domain Hierarchy</mark>

The Domain Hierarchy is structured like an inverted tree with multiple levels, where each level represents a domain, and the entire system is organized from the most general to the most specific. Each part of a domain name corresponds to a level in this hierarchy.

### <mark style="color:purple;">Root Level</mark>

* The top level of the DNS hierarchy.
* Represented as a dot invisible dot (`.`) hidden in domains.
* Is managed by root name servers that direct queries to the appropriate TLD servers.

### &#x20;<mark style="color:purple;">Top-Level Domain (TLD)</mark>

* Is the righthand part of a domain name.&#x20;
* Can only use a-z, 0-9, and hyphens
* Cannot start or end with hyphens or have consecutive hyphens.
* Can be classified into two types:
  * _**gTLD:**_ Generic Top-Level Domain, tell the user the domain name's purpose. For example the `.edu` for education related pages.
  * _**ccTLD:**_ Country Code Top-Level Domain, used for geographical purposes. For example the `.uk` for the United Kingdom pages.

### <mark style="color:purple;">Second-Level Domain (SLD)</mark>

* The most typical part of the domain. Specifies the name of the page.
* Is limited to 63 characters.
* Registered by individuals or organizations through domain registrars.

### <mark style="color:purple;">Subdomain</mark>

* Are optional and normally describe the specific application of a page.
* Can use multiple subdomains but the length must be kept to 253 characters or less.
* There is no limit to the number of subdomains you can create for a domain name.

## <mark style="color:blue;">Record Types</mark>

Define the specific types of information stored about a domain name. Each record type serves a different purpose. Here are the most common DNS record types:

* **A Record (Address):** Resolve to IPv4 addresses.
* **AAAA Record (IPv6 Address):** Resolve to IPv6 addresses.
* **CNAME Record (Canonical Name):** Resolve to another domain name, then the DNS request redirects to the second domain to work out the IP address.
* **MX Record (Mail Exchange):** Resolve to the address of the servers that handle the email for the domain you are querying. Includes a priority flag that tells the client which mail server should be contacted first.
* **NS Record (Name Server):** Indicates the authoritative DNS servers for a domain.
* **TXT Record (Text):** Stores human-readable or machine-readable text. Commonly used for security. Help to list servers that have the authority to send an email on behalf of the domain. Can be used to verify ownership of the domain name when signing up for third-party services.
