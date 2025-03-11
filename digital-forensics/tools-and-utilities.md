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

Here are some tools and utilities commonly used for practices related to digital forensics:

## <mark style="color:green;">Pdfinfo</mark>

* Used to extract metadata of  Portable Document Format (PDF) files

### <mark style="color:yellow;">Commands</mark>

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install poppler-utils
```
{% endcode %}

***

* Read the metadata of a PDF file

{% code overflow="wrap" lineNumbers="true" %}
```bash
pdfinfo $pdffilename
```
{% endcode %}

## <mark style="color:green;">ExifTool</mark>

* Used to extract Metadata from files, especially images

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

* Stenography tool that is used to hide data within image and audio files, and also to recover hidden data embedded in files

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

* Used to delete and overwrite drive or file information in _Linux_

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

* Tool to delete and overwrite drive or file information in _Windows_
* [https://learn.microsoft.com/es-es/sysinternals/downloads/sdelete](https://learn.microsoft.com/es-es/sysinternals/downloads/sdelete)

## <mark style="color:green;">FOCA</mark>

* Fingerprinting Organization with Collected Archives is a tool designed to find metadata and hidden information in documents, analyzing websites as well as Microsoft Office, Open Office, PDF, and other documents
* [https://github.com/ElevenPaths/FOCA](https://github.com/ElevenPaths/FOCA)
