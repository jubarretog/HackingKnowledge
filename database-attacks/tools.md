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

# Tools

## <mark style="color:green;">REDIS</mark>

* Connect to redis client

### Commands

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

***



## <mark style="color:green;">AWS BUBCKET 3</mark>

* S3 Buckets is a service that allos people to save files and even static website content in the cloud accessible over HTTP and HTTPS
* [https://aws.amazon.com/es/s3/](https://aws.amazon.com/es/s3/)

### Commands

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
sudo aws configure #Set evey parameter to temp
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

***



## <mark style="color:green;">MySQL</mark>

* CLI used to connect to _mysql_ databases

### Commands

* Connect to a database

{% code overflow="wrap" lineNumbers="true" %}
```bash
mysql -u $user #Set user
mysql -h $host #Set host
mysql -u $user -h $host -p #Prompt for password
```
{% endcode %}

{% hint style="info" %}
Once you have access you can use _SQL_ queries ot look for information
{% endhint %}

***



## <mark style="color:green;">sqlmap</mark>

* Detect and take advantage of SQL injection vulnerabilities

### Commands

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
sqlmap -r $file.raw --dump --dbs #Detect vulnerabilities and extract information
```
{% endcode %}

***

