# Encoding (WIP)

**Encoding** is the process of transforming data into a different format using a specific scheme to standardize the way data can be stored, transmitted, or interpreted. Unlike encryption, encoding does not provide confidentiality or use a key, but plays a crucial role in compatibility for data exchange across diverse platforms and applications.

Here we find some common encoding methods:

## <mark style="color:blue;">ASCII</mark>

It is a 7-bit encoding standard that represents text using integer values in the 0-255 range. The values between 32-126 are known as printable characters, containing digits, letters, and punctuation values.

Here we find a little function to convert ASCII values into a readable string:

{% code title="ASCII_Decode.py" overflow="wrap" lineNumbers="true" %}
```python
# This script converts ASCII values to a string
def ASCII_to_String(ascii_numbers): #This accepts a list
    recovered = []
    for value in ascii_numbers:
        recovered.append(chr(value))
    recovered = "".join(recovered)
    return recovered

#Usage Example
ascii_numbers = [70, 76, 65, 71, 123, 102, 52, 107, 51, 95, 102, 108, 52, 103, 95, 102, 48, 114, 95, 116, 51, 115, 116, 49, 110, 103, 125]   
print("Recovered String:", ASCII_to_String(ascii_numbers))
```
{% endcode %}

In the same way, here we find a little function to convert a string into ASCII values:

{% code title="ASCII_Encode.py" overflow="wrap" lineNumbers="true" %}
```python
# This script converts a string to ASCII values
def String_to_ASCII(message): #This accepts a string
    ascii = []
    for value in message:
        ascii.append(ord(value))
    return ascii

#Usage Example
message = "FLAG{f4k3_fl4g_f0r_t3st1ng}"
print("Ascii Values:", String_to_ASCII(message))
```
{% endcode %}

We can also find a [table](https://www.rapidtables.com/code/text/ascii-table.html) with all the values and some of their representations.

## <mark style="color:blue;">Hexadecimal</mark>

In this encoding, each letter is converted to an ordinal number according to the ASCII table, then the decimal numbers are converted to base-16 numbers, otherwise known as hexadecimal, and finally, the numbers are combined into one long string.

It's common to use it to encode data for transport in a more portable format, and also to represent bytes that couldn't have printable ASCII values.

Here we find a little script to convert a hex string into bytes:

{% code title="Hex_Decode.py" overflow="wrap" lineNumbers="true" %}
```python
# This script converts a base64 string to a string
def Hex_to_Bytes(hex_value):
    recovered = bytes.fromhex(hex_value)
    return recovered

#Usage Example
hex_value = "464c41477b66346b335f666c34675f6630725f74337374316e677d"
print("Recovered Bytes:", Hex_to_Bytes(hex_value))
```
{% endcode %}

In the same way, here we find a little script to convert bytes into a hex string:

{% code title="Hex_Encode.py" overflow="wrap" lineNumbers="true" %}
```python
# This script converts a string to a base64 string
def Bytes_to_Hex(message):
    hex_string = message.hex()
    return hex_string

#Usage Example
message = "FLAG{f4k3_fl4g_f0r_t3st1ng}"
print("Hex String:", Bytes_to_Hex(message))
```
{% endcode %}

## <mark style="color:blue;">Base64</mark>

This is a representation of binary data as ASCII strings using an alphabet of 64 characters. Each character is passed into bits (each byte provides 8 bits) and then turned into groups of 6 bits to represent a numerical value, which is the new position in the encoding alphabet. In this mode, each 4 characters of Base64 represent three 8-bit bytes.

The string _ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/_ is the alphabet used to encode, and the _=_ symbol is used for padding to ensure the length of the encoded value is a multiple of 4.

Base64 is most commonly used online, so binary data such as images can be easily included in HTML or CSS files.

Here we find a little script to convert a base64 string into bytes:

{% code title="Base64_Decode.py" overflow="wrap" lineNumbers="true" %}
```python
# This script converts a base string into bytes       
import base64

def Base64_to_Bytes(base64_value):
    recovered = base64.b64decode(base64_value)
    return recovered

#Usage Example
base64_value = "RkxBR3tmNGszX2ZsNGdfZjByX3Qzc3Qxbmd9"
print("Recovered Bytes:", Base64_to_Bytes(base64_value))
```
{% endcode %}

In the same way, here we find a little script to convert bytes into a base64 string:

{% code title="Base64_Encode.py" overflow="wrap" lineNumbers="true" %}
```python
# This script converts a string to base64 values
import base64

def Bytes_to_Base64(message):
    base64_string = base64.b64encode(message)
    return base64_string

#Usage Example
message = b"FLAG{f4k3_fl4g_f0r_t3st1ng}"
print("Hex String:", Bytes_to_Base64(message))
```
{% endcode %}

## <mark style="color:blue;">URL</mark>

This i

Here we find a little script to convert a URL string into bytes:

{% code title="URL_Decode.py" overflow="wrap" lineNumbers="true" %}
```python
# This script converts a base string into bytes       
import base64
```
{% endcode %}

In the same way, here we find a little script to convert bytes into a URL string:

{% code title="URL_Encode.py" overflow="wrap" lineNumbers="true" %}
```python
# This script converts a string to base64 values
import base64
```
{% endcode %}

## <mark style="color:blue;">**Morse Code**</mark>

eeee

