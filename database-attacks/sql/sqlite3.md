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

# SQLite3

**SQLite3** is a lightweigh**t**, self-contained, serverless relational database management system that operates on a single file stored locally. It does not require a separate server process, making it ideal for embedded applications, mobile apps, and lightweight data storage.

SQLite3 follows SQL standards and provides ACID-compliant transactions, but it is designed for local storage rather than large-scale or concurrent operations. The entire database is stored in a single file so no server installation or setup is needed and is cross-platform.

The default name for a SQLite3 database is the name of the project with the _.db_ extension, for example, _data.db_ for a project named _data._

## <mark style="color:blue;">Query Syntax</mark>

* To interact with an SQLite database, you can use the command-line tool:

{% code overflow="wrap" lineNumbers="true" %}
```sql
sqlite3 $dbFile # Create or open a database
.tables # List available tables
.schema # Show database schema
SELECT * FROM $tableName; #Retrieve data
PRAGMA table_info(user); #Get information about the columns of a table
.exit #Close connection
```
{% endcode %}
