# Tools

## PDF Info

Used to extract metadata of a pdf file

### Commands

* Installation

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install poppler-utils
```
{% endcode %}

* Read the metadata of a pdf

{% code overflow="wrap" lineNumbers="true" %}
```bash
pdfinfo $pdffilename
```
{% endcode %}

## Exiftool

Used to extract Metadata from files

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt install exiftool
```
{% endcode %}

* Read image EXIF data

{% code overflow="wrap" lineNumbers="true" %}
```bash
exiftool $imagefilename
```
{% endcode %}
