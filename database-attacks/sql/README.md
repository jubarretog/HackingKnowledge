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

# SQL

**Structured Query Language** is the standard language for managing and manipulating relational databases. It allows users to create, read, update, and delete data within a database through simple, structured commands.

<figure><img src="../../.gitbook/assets/image (276) (1).png" alt="" width="375"><figcaption></figcaption></figure>

Mastery of SQL is essential for understanding and manipulating the queries used by systems that utilize this language.

## <mark style="color:blue;">Structure</mark>

We can find that all the SQL Databases have a collection named _Information Schema_ that provides metadata about the database itself and lets us know about the structure of the database, such as tables, columns, data types, views, and user privileges.

It also shows information about all other databases the user has access to. It can be found as _information\_schema_ and is composed of the following structure:

* _**information\_schema.tables**_**:** Tables of the database
  * table\_catalog
  * table\_schem
  * table\_name
  * table\_type
* _**information\_schema.columns**_**:** Information of every column from tables
  * table\_schema: Database where the table is
  * table\_name: Name of the table
  * column \_name: Name of column from a specified table

## <mark style="color:blue;">Queries</mark>

As mentioned earlier, SQL operates by using queries as commands that enable access and execute actions within the DB context. Some of the actions that can be performed include:

* Show databases and tables

{% code overflow="wrap" lineNumbers="true" %}
```sql
show databases;
use $database; #Enter into a database
show tables; #Only after entering a database
```
{% endcode %}

***

* Get a specific column from a query and put it in a string separated by commas

{% code overflow="wrap" lineNumbers="true" %}
```sql
group_concat($column) from $table
group_concat($column SEPARATOR '$separator') FROM $table #AddSeparator for results
```
{% endcode %}

***

* Select data

{% code overflow="wrap" lineNumbers="true" %}
```sql
SELECT * FROM $table;                #Select all columns
SELECT * FROM $table AS $name;       #Get results by choosing a title 
SELECT $column1,$column2 FROM table;  #Select specified columns
SELECT * FROM $table LIMIT$n;        #Limit return to n entries
SELECT * FROM $table LIMIT$n,$n;     #Skip first n values and limit
SELECT * FROM $table WHERE $column='$value';   #Select if match condition
SELECT * FROM $table WHERE $column !='$value'; #Select if don't match condition
SELECT * FROM $table WHERE $column1='$value'or $column2='$value'  #OR Condition
SELECT * FROM $table WHERE $column1='$value'and $column2='$value' #AND Condition
SELECT * FROM $table WHERE $column LIKE '$value%';  #Select if starts with value
SELECT * FROM $table WHERE $column LIKE '%$value';  #Select if ends with value
SELECT * FROM $table WHERE $column LIKE '%$value%'; #Select if contains value
SELECT * from $table;-- #Specified everything after -- will be taken as comment
```
{% endcode %}

***

* Select data from multiple tables

{% code overflow="wrap" lineNumbers="true" %}
```sql
SELECT * FROM $table1 UNION SELECT * FROM $table2;    #Combine results
```
{% endcode %}

***

* Insert data

<pre class="language-sql" data-overflow="wrap" data-line-numbers><code class="lang-sql"><strong>INSERT INTO $table ($column1,$column2) VALUES ('$value1','$value2');
</strong></code></pre>

***

* Update data

{% code overflow="wrap" lineNumbers="true" %}
```sql
UPDATE $table SET $column1='$value1',$column2='$value2' WHERE $column='$value';
```
{% endcode %}

***

* Delete  data

{% code overflow="wrap" lineNumbers="true" %}
```sql
DELETE FROM $table; #Delete all rows
DELETE FROM $table where username='martin'; #Delete all rows that match condition
```
{% endcode %}
