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

# Useful Tips

Here we can find some tips for maximizing the use of information-gathering concepts, tools, and utilities:

* Make an initial port scan when you connect to a target machine
* Check well-known ports of protocols
* Check the _TTL_ value when doing `ping` to a machine, to determine what operating system the machine is associated with
* On HTTPS sites check the certificate to gather information about the encryption and the server
* Check DNS records to gather information about host names, domains and
* Use `host` command to get domains and IP address information, and then pass it to `whois` command, to identify if a service is self-hosted or is using cloud services
* Examine SSL certificates from websites to obtain information about domains, use tools such as [_crt.sh_](tools-and-utilities.md#crt.sh)
* Check the DNS records of a host using commands like `whois`, `host` and `dig`&#x20;
* Check default configuration files for network services like:
  * _/etc/samba/smb.conf_ for SMB configurations
  * _/etc/exports_ for NFS configuration
  * _/etc/vsftpd.conf_ for FTP configuration
  * _/etc/bind/named.conf.local_ for DNS configuration
    * _/etc/bind/db.$domain_ or _/etc/bind/db.$IP_ for DNS zone files
  * _/etc/postfix/main.cf_ for SMTP configuration
  * _/etc/snmp/snmpd.conf_ for SNMP configuration
  * /etc/mysql/mysql.conf.d/mysqld.cnf for MYSQL configuration
