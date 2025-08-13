# Fundamental Concepts

## <mark style="color:blue;">Bytes Representation</mark>

Bytes represent raw binary data used to manipulate, inspect, and convert values at a low level. The printable bytes are usually represented directly as ASCII, but the non-printable, are shown in a raw way using a hexadecimal value between 0-255 and with the `\x` prefix,  for example, `\x00` for the null byte.

Here we find a little script with some examples of byte manipulation:

{% code title="Bytes.py" overflow="wrap" lineNumbers="true" %}
```python
# We can observe its representation
print("Raw Byte:", b'\x00') # Raw byte that is not printable
print("Printable Byte:", b'\x41') # Raw byte but is printed as 'A'

# We can obtain an int value with the position in the 0-255 range
byte1 = b'B'
print("Byte Value:", byte1[0])

# For byte strings, we could do the same with the byte at any position
byte_str = b'flag'
print("String Byte Values:", byte_str[0],byte_str[1],byte_str[2],byte_str[3])

# We can concatenate bytes, or operate on them using their int representation 
byte1 = b'\x03'
byte2 = b'\x02'
print("Concatenate:", byte1 + byte2)
print("Result Value:", byte1[0] + byte2[0]) # This return and the result int
print("Result Bytes:", bytes([byte1[0] + byte2[0]])) # This converts the result again in bytes

# As bytes only are in the 0-255 range, we could have errors outside this range
b1 = b'\xf0'  # Its value is 240
b2 = b'\x3f'  # Its value is 63
add = b1[0] + b2[0]  # The result is 303, out of the range

# We can use the modular operator to truncate results in the range
add = add % 256 # Now, the result is b'\x47' which is b'/'
print("Result in range:", bytes([add]))
```
{% endcode %}

## <mark style="color:blue;">Long Integer Representation</mark>

Bytes can be represented as long numerical values to use them for mathematical operations.

Here we find a little script to convert bytes into long integers:

{% code title="Bytes_to_Long.py" overflow="wrap" lineNumbers="true" %}
```python
# This script converts bytes into a long     
from Cryptodome.Util.number import bytes_to_long

def Bytes_to_Long(message):
    long_number = bytes_to_long(message)
    return long_number

#Usage Example
message = b"FLAG{f4k3_fl4g_f0r_t3st1ng}"
print("Integer Representation:", Bytes_to_Long(message))
```
{% endcode %}

In the same way, here we find a little script to convert integers into bytes:

<pre class="language-python" data-title="Long_to_Bytes.py" data-overflow="wrap" data-line-numbers><code class="lang-python"># This script converts a long into bytes       
<strong>from Cryptodome.Util.number import long_to_bytes
</strong>
def Long_to_Bytes(long_number):
    recovered = long_to_bytes(long_number)
    return recovered

#Usage Example
long_number = 28918866808831822367805849580817521177463833928225773799944906621
print("Recovered Bytes:", Long_to_Bytes(long_number))
</code></pre>

## <mark style="color:blue;">XOR Operation</mark>

It is a bitwise operator that returns 0 if the bits are the same, and 1 otherwise. It is usually denoted by the ⊕ symbol in math, but in most programming languages it is represented with the `^` symbol.

### <mark style="color:purple;">Properties</mark>

* **Involution:** Making XOR to a value twice with the same key, returns the original value.\
  For example:   _A^B = C_  &#x20;  ⇔   _C^B = A_
* **Commutation:** The order of the XOR operands does not affect the result of the operation.\
  For example:   _A^B = B^A_
*  **Associative:** A chain of operations can be carried out without order, and the result will be the same.\
  For example:   _A^(B^C) = (A^B)^C_
*  **Identity:** The identity is _0_, so XOR anything with _0_ does not change the original value.\
  For example:   _A^0 = A_   or   _A^\x00 = A_   if we are working with bytes
* **Self-Inverse:** Making an XOR between any value and itself returns the identity (_0_).\
  For example:   _A^A = 0_

### <mark style="color:purple;">Implementation</mark>

Here we find some explanations and scripts to apply this operation:

* For int and hex, they are first represented in binary, and then the XOR operation is done bit by bit

<pre class="language-python" data-overflow="wrap" data-line-numbers><code class="lang-python"># This script performs an XOR operation between numbers or hex

<strong>def XOR_Int(num1,num2):
</strong><strong>    result = num1 ^ num2
</strong><strong>    return result
</strong><strong>
</strong>def XOR_Hex(hex1, hex2):
    result = hex1 ^ hex2
    return hex(result)
<strong>
</strong><strong>#Usage example
</strong><strong>num1, num2 = 13, 11 # Xoring 1101 ^ 1011 = 0110 which is 6
</strong><strong>print("Result Int:", XOR_Int(num1, num2))
</strong>hex1, hex2 = 0x1F, 0xF0 # Xoring 00011111 ^ 11110000 = 11101111 which 0xEF
print("Result Hex:", XOR_Hex(hex1, hex2))
</code></pre>

***

* For characters or bytes, they have to be converted to their ASCII values first, and then the XOR is applied to these values. For strings, we have to represent them as bytes and then loop through the previous process for each character

<pre class="language-python" data-overflow="wrap" data-line-numbers><code class="lang-python"># This script performs an XOR operation between characters or strings
from Cryptodome.Util.number import long_to_bytes

def XOR_Char(char1,char2):
    result = ord(char1) ^ ord(char2)
    return long_to_bytes(result)

def XOR_String(str1, str2):
    result = bytes([a ^ b for a, b in zip(str1, str2)])
    return result

#Usage example
char1 = b'A' # ASCII 65  → 01000001
char2 = b'z' # ASCII 122 → 00111011
<strong>print("Result Char:", XOR_Char(char1,char2)) # Result 00111011 → 59 which is ";"
</strong>str1 = "flag1"
str2 = "flag2"
print("Result String:", XOR_String(str1.encode(), str2.encode())) # Used as bytes
</code></pre>

***

* To make it easier and operate between data types, we can use the `xor()` function from the _pwntools_ Python library

{% code overflow="wrap" lineNumbers="true" %}
```python
# This script performs an XOR operation between different data types
from pwn import xor

xored = b'KALJvk9f>Rka9jRk=\x7fRy>~y<cjp'
print("Result", xor(xored, 13))
```
{% endcode %}
