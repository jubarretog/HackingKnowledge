# Related Concepts

* **Directory:** A hierarchical database containing all information and definitions of objects, such as users, groups, computers, and other resources, and their relationships within an organization
* **Domain:** A logical entity that groups a set of objects under a single security policy and database
* **ACL:** Access Control List is a set of permissions that defines who can do what to a specific AD object. It’s not an object like a user or group, but rather metadata attached to objects in the directory
* **GPO:** Group Policy Object is a set of policy settings that can be applied to objects within a domain. Control a variety of settings, from security policies to software configurations
* **SAM:** Security Account Manager is a local database on every Windows machine that stores local user accounts, groups, password hashes (NTML), and security identifiers (SIDs). It handles authentication and access control for local accounts
* **KDC:** Key Distribution Center acts as the central authority in the Kerberos authentication process, issuing access tickets that validate the identity of users and services within the network
* **Client:** The entity requesting access to a resource
* **Service:** A resource that requires Kerberos authentication
* **SPN:** Service Principal Name is a unique ID used to identify services in the domain
* **PAC:** It carries detailed information that allows the application servers to know the rights and privileges of a user. It may or may not be included in TGT and TGS tickets
* **Realm:** It is an administrative domain for Kerberos, generally corresponding to a domain in a network
*   **S4U2self:** Kerberos extension that allows a service to obtain a ticket for a specific user, even if the user is not logged in, usually where a service needs to act on behalf of a user

    **S4U2proxy:** Kerberos extension that allows a service to use a ticket obtained through S4U2self to request additional tickets to access other services on behalf of the user
