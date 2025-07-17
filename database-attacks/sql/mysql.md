# MySQL

**MySQL** is a widely used open-source relational database management system that operates using the client-server model over the Application layer, usually on port 3306. It is primarily used for storing, managing, and retrieving structured data efficiently and implements a client-server model.

Its main features are:

* Can use SSL/TLS for secure, encrypted connections
* Manages structured data with SQL queries
* Supports transactions, indexing, and stored procedures
* Allows remote and local database access for applications

Query syntax is the standard [SQL](./) syntax for simplicity.

## <mark style="color:blue;">Interaction and Query Syntax</mark>

* We use the command line utility to connect to a database, and once inside, we use standard SQL queries

{% code overflow="wrap" lineNumbers="true" %}
```bash
mysql -u $user #Set user
mysql -h $host #Set host
mysql -u $user -h $host -p #Prompt for password
mysql -u $user -h $host -p #Prompt for password
mysql -u $user -h $host --skip-ssl #Don't use SSL for the connection
```
{% endcode %}
