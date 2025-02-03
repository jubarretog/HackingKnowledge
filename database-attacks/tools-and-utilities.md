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

# Tools and Utilities

Here are some tools and utilities commonly used for practices related to database attacks:

## <mark style="color:green;">redis-cli</mark>

* A utility used to connect to Redis databases using the command line

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install redis
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo redis-cli
sudo redis-cli -h $hostname #Specify hostname
```
{% endcode %}

## <mark style="color:green;">awscli</mark>

* A utility used to connect to AWS services using the command line
* It could interact with services such as S3 buckets

### <mark style="color:yellow;">Commands</mark>

* Install amazon cli

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install awscli
```
{% endcode %}

***

* Configure amazon

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo aws configure #Set every parameter to temp
```
{% endcode %}

***

* Access to s3 service

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo aws --endpoint=http://$url s3 $command #Execute a command on the bucket
sudo aws --endpoint=http://$url s3 ls #List buckets
sudo aws --endpoint=http://$url s3 ls s3://$listedurl #Lists elements in the bucket
sudo aws --endpoint=http://$url s3 cp $file s3://$listedurl #Upload a file to a bucket
```
{% endcode %}

## <mark style="color:green;">mysql</mark>

* CLI used to connect to MySQL databases

### <mark style="color:yellow;">Commands</mark>

* Connect to a database

{% code overflow="wrap" lineNumbers="true" %}
```bash
mysql -u $user #Set user
mysql -h $host #Set host
mysql -u $user -h $host -p #Prompt for password
```
{% endcode %}

{% hint style="info" %}
Once having access, we can use SQL queries to look for information
{% endhint %}

## <mark style="color:green;">sqlmap</mark>

* Detect and take advantage of SQL injection vulnerabilities

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install sqlmap
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
sqlmap -u $URL #Show the sqli vulnerabilities
sqlmap -u "$URL" --dbms $dbname #Specify what database is
sqlmap -r $file.raw #Use a raw petition to set target information
sqlmap -r $file.raw --dump --dbs #Extract information of the databases
sqlmap -r $file.raw --dump --tables #Extract information of the tables
sqlmap -r $file.raw --dump -T $table #Extract information of an specific table
sqlmap -r $file.raw --level $level #Specify intensity level of the attack
```
{% endcode %}

## <mark style="color:green;">Mongocli</mark>

* Utility for connecting to MongoDB databases via the command line

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install mongocli
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
mongo --port $port
```
{% endcode %}

## <mark style="color:green;">Mongosh</mark>

* Adapted utility for connecting to [_MongoDB_](https://www.mongodb.com/) databases via the command line, similar to [_Mongocli_](tools-and-utilities.md#mongocli) but with some extra options

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
curl -O https://downloads.mongodb.com/compass/mongosh-2.3.2-linux-x64.tgz
tar xvf mongosh-2.3.2-linux-x64.tgz
mv ./bin/mongosh /usr/local/bin
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
mongosh mongodb://$IP:$PORT
```
{% endcode %}

## <mark style="color:green;">PostgreSQL</mark>

* Command line utility used to connect or interact with [_PostgreSQL_](https://www.postgresql.org/) databases

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install postgresql
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
psql -h $IP #Connect to the PostgreSQL service
psql -h $IP -p $port #Connect specifying a port
psql -h $IP -U $username #Connect specifying a user
```
{% endcode %}
