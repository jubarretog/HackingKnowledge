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

Here we can find some tools and utilities commonly used for processes related to digital forensics:

## <mark style="color:green;">PDF Info</mark>

* Used to extract metadata of a PDF file

### <mark style="color:yellow;">Commands</mark>

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

## <mark style="color:green;">ExifTool</mark>

* Used to extract Metadata from files, especially image

### <mark style="color:yellow;">Commands</mark>

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

## <mark style="color:green;">Steghide</mark>

* Stenography tool that is used to hide data within image and audio files, and also to recover hidden data embedded in files.

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install steghide
```
{% endcode %}

***

* Handle embedded data

{% code overflow="wrap" lineNumbers="true" %}
```bash
steghide info $filename #Get info from embedded data
steghide extract -sf $filename #Extract data from file
```
{% endcode %}

## <mark style="color:green;">d4js</mark>

* Used to deobfuscated JavaScript code
* [https://lelinhtinh.github.io/de4js/](https://lelinhtinh.github.io/de4js/)

## <mark style="color:green;">Shred</mark>

* Used to delete and overwrite drive or file information in Linux

### <mark style="color:yellow;">Commands</mark>

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install coreutils
```
{% endcode %}

***

* Usage

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo shred $filename
sudo shred $filename -f     #Change permissions to allow overwriting
sudo shred $filename -n $n  #Specify number of times to overwrite
sudo shred $filename -v     #Verbose mode, show step-by-step
sudo shred $filename -u     #Truncate and eliminate file after overwriting
sudo shred $filename -z     #Overwrite with 0
sudo shred -vu /dev/$unit   #Delete a memory unit or partition
```
{% endcode %}

## <mark style="color:green;">SDelete</mark>

* Tool  to delete and overwrite drive or file information in Windows
* [https://learn.microsoft.com/es-es/sysinternals/downloads/sdelete](https://learn.microsoft.com/es-es/sysinternals/downloads/sdelete)