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

The **Domain Name System** protocol acts like a phonebook for the Internet by translating human-friendly domain names into IP addresses, being a critical part of how the Internet functions. It  operates in the Application layer usually on UDP port 53

For example, when users enter a domain name in their browser such as _google.com_, the DNS queries multiple servers to resolve the name into the corresponding IP address _8.8.8.8_ related to this domain. It's also possible that various IP addresses are related to the same domain name.

## <mark style="color:blue;">Work Flow</mark>

* A computer makes a DNS Query to ask for the IP of a domain, first checking the cache and then reaching out to a DNS resolver
* The DNS Resolver makes a recursive lookup through the domain Hierarchy until finding the corresponding IP or hitting the root server.
* Root Name Server indicates which server knows the IP and points the resolver in that direction passing through the TLD Name Server and reaching the corresponding Authoritative Name Server
* The authoritative name sends back the correct IP to the resolver which gives it to the computer. This is saved on the caches to remember it in the short term, and finally, the computer connects directly to the web server hosting the application

## <mark style="color:blue;">Domain Types</mark>

* **Authoritative Nameserver:** Hold authority for a particular zone, only answer queries from their area of responsibility, and their information is binding. If an authoritative name server cannot answer a client's query, the root name server takes over at that point
* **Non-authoritative Nameserver:** Not responsible for a particular DNS zone, they collect information on specific DNS zones themselves, which is done using recursive or iterative DNS querying
* **Caching DNS Server:** Cache information from other name servers for a specified period. The authoritative name server determines the duration of this storage
* **Forwarding Server:** Forward DNS queries to another DNS server
* **Resolver:** Non-authoritative DNS server that performs name resolution locally in a computer or router

## <mark style="color:blue;">Domain Hierarchy</mark>

The Domain Hierarchy organizes domain names on the Internet. It is structured like an inverted tree with multiple levels, where each level represents a domain, and the entire system is organized from the most general to the most specific. Each part of a domain name corresponds to a level in this hierarchy.

### <mark style="color:purple;">Root Level</mark>

* The top level of the DNS Hierarchy
* Represented as a dot invisible `.` hidden in domains
* Is managed by root name servers that direct queries to the appropriate TLD servers
* There are just 13 root servers in the world

### &#x20;<mark style="color:purple;">Top-Level Domain (TLD)</mark>

* Is the righthand part of a domain name
* They can only be composed of a-z, 0-9, and hyphens, and can't start or end with hyphens or have consecutive hyphens
* Can be classified into two types:
  * _**gTLD:**_ Generic Top-Level Domain, tell the user the domain name's purpose, for example, the _.edu_ domain for sites related to education
  * _**ccTLD:**_ Country Code Top-Level Domain, used for geographical purposes, for example, the _.uk_ for the sites from the United Kingdom

### <mark style="color:purple;">Second-Level Domain (SLD)</mark>

* Also known as Autorithative Name Server
* Is the most typical part of the domain which specifies the name of the page
* Consist of a maximum of 63 characters
* They are registered by individuals or organizations through domain registrars

### <mark style="color:purple;">Subdomain</mark>

* Are optional and normally describe the specific application of a page
* Can use multiple subdomains but the length must be kept to 253 characters or less
* There is no limit to the number of subdomains you can create for a domain name

## <mark style="color:blue;">Record Types</mark>

The records are entries in a DNS server that map domain names to IP addresses and other information. They have some types that define specific classes of information stored about a domain name, each one serving a different purpose. Here are the most common DNS record types:

* **A Record (Address):** Resolve to IPv4 addresses
* **AAAA Record (IPv6 Address):** Resolve to IPv6 addresses
* **CNAME Record (Canonical Name):** Resolve to another domain name, then the DNS request redirects to the second domain to work out the IP address
* **MX Record (Mail Exchange):** Resolve to the address of the servers that handle the email for the domain you are querying. Includes a priority flag that tells the client which mail server should be contacted first
* **NS Record (Name Server):** Indicates the authoritative DNS servers for a domain
* **TXT Record (Text):** Stores human-readable or machine-readable text. Commonly used for security. Help to list servers that have the authority to send an email on behalf of the domain. Can be used to verify ownership of the domain name when signing up for third-party services
* **PTR Record (Pointer):** Applies reverse lookup to convert IP addresses into valid domain names
* **SOA Record (Start of Authority):** Provides information about the corresponding DNS zone and email address of the administrative contact
* **SRV Record (Service):**  Defines the hostname and port number for specific services
