# SQL

## Information Schema

DB that save information about all other DB the user has access, find as **`information_schema`**

* **`.tables`:** Tables of DB
  * table\_catalog
  * table\_schem
  * table\_name
  * table\_type
* **`.columns`:** Information of every column from tables.
  * table\_schema: DB where table is.
  * table\_name: Name of the table.
  * column \_name: Name of column from a specified table.



## Commands

* Show database name

<pre class="language-sql" data-overflow="wrap" data-line-numbers><code class="lang-sql"><strong>database();
</strong></code></pre>

***

* Get an Specified column from a query and put it in a string separated by commas

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

***

