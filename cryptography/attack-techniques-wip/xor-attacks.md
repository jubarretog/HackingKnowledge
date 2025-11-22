# XOR Attacks

Here we find some scripts that could help us do XOR attacks in different scenarios:

* The message was XORed with the same unique byte

{% code title="XOR_1-Byte.py" overflow="wrap" lineNumbers="true" %}
```python
from pwn import xor

enc = "616b66605c41134c1478414b13407841175578531454531649405a"
enc = bytes.fromhex(enc)

flag = b""
for key in range(256):
	xored = xor(enc,key)
	if xored.startswith(b"FLAG{"):
		print("Key found:", bytes([key]))
		flag = xored
		break

print("Flag:", flag)
```
{% endcode %}

***

* The message was XORed with an unknown string, but we know the start of the plaintext

{% code title="XOR_Start.py" overflow="wrap" lineNumbers="true" %}
```python
from pwn import xor

enc = "0b350a22022b4d2056262b157f02262b49393a0d7e0a3f54172a04"
enc = bytes.fromhex(enc)
known = b"FLAG{"

# known ^ secret = enc  <--->  enc ^ known = secret
secret = xor(enc[:len(known)], known) # XOR as much bytes as we know
print("Secret Key:", secret)
print("Flag:", xor(enc, secret))

# Via brute-forcing
secret = b""
for i in range(len(known)):
	for key in range(256):
		xored = xor(enc[i],key)                          
		if xored == bytes([known[i]]):
			secret += bytes([key])
			break

print("Secret Key:", secret)
print("Flag:", xor(enc, secret))
```
{% endcode %}

{% hint style="warning" %}
These will only leak as many bytes of the key as we know of the plaintext
{% endhint %}
