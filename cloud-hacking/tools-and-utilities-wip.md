# Tools and Utilities (WIP)

Here we can find some tools and utilities commonly used for practices related to Cloud Hacking:

## <mark style="color:green;">awscli</mark>

* A utility used to connect to AWS services using the command line
* It could interact with services such as S3 buckets

### <mark style="color:yellow;">Commands</mark>

* Install Amazon CLI

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

* Access to the S3 service

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo aws --endpoint=http://$url s3 $command #Execute a command on the bucket
sudo aws --endpoint=http://$url s3 ls #List buckets
sudo aws --endpoint=http://$url s3 ls s3://$listedurl #Lists elements in the bucket
sudo aws --endpoint=http://$url s3 cp $file s3://$listedurl #Upload a file to a bucket
```
{% endcode %}
