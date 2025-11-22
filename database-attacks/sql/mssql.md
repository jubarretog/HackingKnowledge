# MSSQL

**Microsoft SQL Server** is a relational database management system that operates by default on port 1433, used for managing and querying structured data in enterprise environments.

MSSQL enables secure and efficient database operations, supporting Transact-SQL for querying and database management. It provides features like data storage, high availability, backup and recovery, and authentication mechanisms.

Its main features are:

* Allows TLS/SSL encryption for secure database connections
* Role-based Access Control for specifying user permissions
* Set firewall rules to control external access to the SQL server
* Tracks database access and query execution for security monitoring

To interact with the service, we can use tools such as the _mssqlclient_ utility, which is part of the [_Impacket_](../../networks/tools-and-utilities.md#impacket) toolkit.

## <mark style="color:blue;">Interaction and Query Syntax</mark>

* MSSQL uses standard SQL with a few variants for some commands

{% code overflow="wrap" lineNumbers="true" %}
```sql
SELECT name FROM sys.databases; #Show databases
SELECT name FROM sys.tables; #Show tables
USE $databaseName; #Select a database
SELECT * FROM table $tableName; #Get all the information from a table
```
{% endcode %}
