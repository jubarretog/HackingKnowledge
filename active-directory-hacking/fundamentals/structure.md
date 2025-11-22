# Structure

Active Directory is built on a multi-level hierarchical model, divided into logical and physical structures.&#x20;

<figure><img src="../../.gitbook/assets/image (942).png" alt=""><figcaption><p><a href="https://www.dispersednet.com/active-directory/module2/images/adstructure.gif">https://www.dispersednet.com/active-directory/module2/images/adstructure.gif</a></p></figcaption></figure>

The logical structure defines how resources are organized and managed:

* **Objects:** They are the basic units in AD. They could be:
  * **Users:** Represent individual user accounts
  * **Computers:** Represent machines joined to a domain
  * **Groups:** Collections of users/computers for simplified permission management
  * ACLs
* **Organizational Unit (OU):** A sub-container within a domain. It is used to logically group users, groups, or computers and allows the delegation of resources and the application of group policies
* **Domain:** A core administrative unit that stores all directory objects (users, groups, computers). Shares a common database, security policies, and trust relationships. Domains within a forest are connected via transitive two-way trusts
* **Trees:** A collection of one or more domains that share a contiguous namespace and hierarchical structure
* **Forest:** The highest-level container, which represents a security boundary. Contains one or more trees that share a common schema and a global catalog. Trusts can be established between forests
* **Schema:** Is the framework that defines what kinds of objects can exist in the directory, and what characteristics those objects can have, defining classes, and rules

In short, several objects using the same database can be grouped into a single domain, multiple domains can be combined into a single tree, and multiple trees can be grouped into a forest. Each of these levels can be assigned specific access rights and communication privileges

On the other hand, the physical structure maps to the actual hardware and network topology:

* **Domain Controller (DC):** A server that hosts a read/write copy of the AD database. Handles authentication, authorization, replication, and directory lookups for an assigned domain
* **Sites:** Reflect the network topology of an organization. Comprised of well-connected IP subnets, used to optimize replication traffic and client logon performance
*   **Global Catalog Servers:** DCs that store a partial replica of all domain objects across the forest.

    Enable universal group membership resolution and cross-domain searches

## <mark style="color:blue;">GPOs and ACLs</mark>

These two are fundamental for the security management of the Active Directory, each with its own level of impact.

* **GPO:** Group Policy Object is a configuration policy in Active Directory that allows administrators to centrally manage settings for users and computers across the network. The main features are:
  * Contains registry-based settings, scripts, software installation policies, and security settings
  * Can be linked to sites, domains, or Organizational Units
  * Applies to users and/or computers within the scope of the link
  * Enforced by the Group Policy Client Service running on Windows machines.
* **ACL:** An Access Control List is a security descriptor attached to every object in Active Directory (and in the file system) that defines who can access the object and what operations they can perform. The main features are:
  * Contains Access Control Entries (ACEs) that grant or deny rights
  * Used to control permissions on objects (users, groups, OUs, GPOs), files, folders, registry keys, or even services
  * They can be found in two types:
    * **DACL:** Discretionary ACL, which defines access permissions
    * **SACL:** System ACL, which defines audit settings that also trigger logs

## <mark style="color:blue;">Default Active Directory Groups</mark>

* **Domain Admins:** This group has full control over all domains in a forest. Any user in this group can make any changes to the domain and its objects
* **Enterprise Admins:** Members of this group have permissions to make enterprise-wide changes, including all domains and forests
* **Schema Admins:** Users in this group can make changes to the AD schema with all its objects and attributes
* **Account Operators:** Can administer user accounts and groups within a domain, but cannot modify the members of administrator groups or change the configuration of domain servers
* **Backup Operators:** Can perform backups and restore files on a server, regardless of access permissions
* **Server Operators:** Can perform maintenance tasks on domain servers
* **Guests:** By default, they have minimal privileges and are generally used to provide temporary or limited access to the network
* **DNS Admins:** A special group that has administrative privileges over the domain's DNS service
