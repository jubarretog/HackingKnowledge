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

## <mark style="color:green;">PDF Info</mark>

Used to extract metadata of a pdf file

### Commands

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install poppler-utils
```
{% endcode %}

***

* Read the metadata of a pdf

{% code overflow="wrap" lineNumbers="true" %}
```bash
pdfinfo $pdffilename
```
{% endcode %}

***



## <mark style="color:green;">Exiftool</mark>

Used to extract Metadata from files, specially image

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install exiftool
```
{% endcode %}

***

* Read EXIF data

{% code overflow="wrap" lineNumbers="true" %}
```bash
exiftool $filename
```
{% endcode %}

***



## <mark style="color:green;">Steghide</mark>

Stenography Program

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt-get install steghide
```
{% endcode %}

***

* Commands

{% code overflow="wrap" lineNumbers="true" %}
```bash
steghide info $filename #Get info of embedded data
steghide extract -sf $filename #Extract data from file
```
{% endcode %}

***



## <mark style="color:green;">Shred</mark>

Used to delete and overwrite a drive information in Linux

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo shred $filename
sudo shred $filename -f     #Change permissions to allow overwritting
sudo shred $filename -n $n  #Specify number of times to overwrite
sudo shred $filename -v     #Verbose mode, show step by step
sudo shred $filename -u     #Truncate and eliminate file after overwriting
sudo shred $filename -z     #Overwrite with 0
sudo shred -vu /dev/$unit   #Delete a memory unit or partition
```
{% endcode %}

***



## <mark style="color:green;">SDelete</mark>

Tool  to delete and overwrite a drive information in Windows

* [https://learn.microsoft.com/es-es/sysinternals/downloads/sdelete](https://learn.microsoft.com/es-es/sysinternals/downloads/sdelete)

