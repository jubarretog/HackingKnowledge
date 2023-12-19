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
sudo aws --endpoint=http://$url s3 $command
sudo aws --endpoint=http://$url s3 ls #List buckets
sudo aws --endpoint=http://$url s3 ls s3://$listedurl #Lists elements in the bucket
sudo aws --endpoint=http://$url s3 cp $file s3://$listedurl #Upload a file to a bucket
```
{% endcode %}

***



## <mark style="color:green;">MySQL</mark>

* Connect to mysql

{% code overflow="wrap" lineNumbers="true" %}
```bash
mysql -u $user -h $host -p #Prompt for password
```
{% endcode %}

***

