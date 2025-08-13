---
layout:
  width: default
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
  metadata:
    visible: true
---

# Modular Arithmetic (WIP)

It is a mathematical system that deals with integers and their remainders when divided by a specific positive number, known as the **modulo**.&#x20;

Instead of traditional arithmetic, where numbers can grow indefinitely, modular arithmetic operates on the principle of congruenc&#x65;**,** which gives a cyclic behavior to the numerical groups limited by the modulus value.

It enables operations over bounded sets, supports cyclic structures, and ensures that results stay within predictable limits, making it ideal for environments with constraints on data size.

It is implemented in many areas of computer science and cryptography, particularly in:

* Hashing algorithms
* Checksums and error detection
* Cryptographic protocols like RSA and Diffie-Hellman
* Finite fields in elliptic curve cryptography

Here we explore some important concepts for this subject:

## <mark style="color:blue;">Operations</mark>

* **Modulo Operator:** It is understood as the remainder of the division
  * $$a \bmod n$$
  * Example: $$7 \bmod 3 = 1$$ because $$7/3 = 2$$ and its remainder is $$1$$
* **Addition:** Perform subtraction, then apply the modulo
  * $$(a + b) \bmod n$$
  * Example: $$(7+9) \bmod 10 = 16 \bmod 10 = 6$$
* **Subtraction:** Perform subtraction, then apply modulo. If the result is negative, we wrap it around by adding $$n$$ to maintain it within the boundaries of the modulo
  * $$(a - b) \bmod n$$
  * Example: $$(4-7) \bmod 5 = -3 \bmod 5 = (-3+5) \bmod 5 = 2 \bmod 5 = 2$$
* **Multiplication:** Multiply first, then apply modulo
  * $$(a⋅b)  \bmod  n$$
  * Example: $$(3⋅4)  \bmod  5 = 12  \bmod 5 = 2$$
* **Exponentiation:** Repeated multiplication with modulo applied at each step
  * $$(a^b) \bmod n$$
  * Example: $$3^4 \bmod  5 = 81  \bmod  5 =13^4 \bmod 5 = 81 \bmod 5 = 134mod5=81mod5=1$$

## <mark style="color:blue;">Greatest Common Divisor (GCD)</mark>

The GCD is the largest number that divides two positive integers. For example, with $$a=16$$, and $$b=12$$ the divisors of $$a$$ are $$\{1,2,3,4,6,12\}$$ and the divisors of $$b$$ are $$\{1,2,4,8\}$$. Comparing these two, we see that $$gcd⁡(a,b)=4$$

If the $$gcd⁡(a,b)=1$$ for any pair of integer numbers $$a$$ and $$b$$, we say that they are **coprime** numbers. This works in a particular way for prime numbers, as they only have themselves and $$1$$ as divisors, the $$gcd⁡(a,b)=1$$ everytime, so they will always be coprime.

Also, we note that if $$a$$ is prime and $$b < a$$, then a and b are always coprime, because $$a$$ won't have any divisors lower than itself, but this won't always be true the other way ($$b>a$$).

### <mark style="color:purple;">Calculating GCD with Code</mark> <a href="#firstheading" id="firstheading"></a>

* Iterating from 1 to the smaller of the two numbers and checking which numbers divide both

{% code overflow="wrap" lineNumbers="true" %}
```python
def gcd(a, b):
    gcd = 1
    for i in range(1, min(a, b) + 1):
        if a % i == 0 and b % i == 0:     # Check if the remainder of both is 0
            gcd = i
    return gcd

print("Enter two numbers to find their GCD:")
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))
print(" The GCD is:", gcd(a, b))
```
{% endcode %}

***

* Using _Python_ libraries for optimized versions

{% code overflow="wrap" lineNumbers="true" %}
```python
import math

print("Enter two numbers to find their GCD:")
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))
print(" The GCD using math is:", math.gcd(a, b))
```
{% endcode %}

***

* Using _SageMath_ for optimized versions

{% code overflow="wrap" lineNumbers="true" %}
```python
from sage.all import *

print("Enter two numbers to find their GCD:")
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))
print(" The GCD using math is:", gcd(a, b))
```
{% endcode %}

## <mark style="color:blue;">Congruence</mark>

Two integers $$a$$ and $$b$$ are said to be congruent modulo $$n$$, if they leave the same remainder when divided by $$n$$. This is written as $$a \equiv b \bmod n$$

This could be understood in different ways:

* $$a$$ and $$b$$ have the same remainder when divided by $$n$$.\
  For example,$$14 \equiv 5 \bmod 3$$  because $$14 \bmod 3 = 2$$ and $$5 \bmod 3 = 2$$
* $$a$$ and $$b$$ are congruent modulo $$n$$ because $$a-b$$ is divisible by $$n$$\
  With the valuces, $$14 \equiv 5 \bmod 3$$ because $$14-5 = 9$$, and $$9$$ is divisible by $$3$$
* Exits a value $$k$$ that satisfies $$n*k = a-b$$\
  In the same way, $$14$$ is congruent with $$5$$ modulo $$3$$ because with $$k=3$$ it satifies $$3*3 = 14-5$$

### <mark style="color:purple;">Congruence Equations</mark>

To find the value of  $$b$$ in an equation $$a \equiv b \bmod n$$ we just have to solve $$a \bmod n$$

<pre class="language-python" data-overflow="wrap" data-line-numbers><code class="lang-python"># Example for 8146798528947 ≡ b mod 17
b = 8146798528947 % 17
print(b)    # Result is 4
<strong>
</strong><strong># Or with sage
</strong><strong>from sage.all import *
</strong><strong>
</strong><strong>b = mod(8146798528947, 17)
</strong><strong>print(b)
</strong></code></pre>

This found value works as $$b + nk$$ for any $$k$$ value and the congruence will still be satisfied

For example, $$14 \equiv b \bmod 3$$ is solved $$b=2$$ because $$14 \bmod 3 = 2$$ which lets us with $$14 \equiv 2 \bmod 3$$

* If we use $$k=1$$ we have $$2 + (3 \cdot 1) = 5$$ and this lets us with $$14 \equiv 5 \bmod 3$$ which is true
* Now, with $$k=2$$ we have $$2 + (3 \cdot 1) = 2$$ and this lets us with $$14 \bmod 3 = 2$$ which is  also true
* And so on with any $$k$$ value

***

To find the value of $$n$$ in an equation $$a \equiv b \bmod n$$ we just have to solve $$a-b$$ and any of its divisors will work.

{% code overflow="wrap" lineNumbers="true" %}
```python
def divisors(d):
    divs = []
    for i in range(1, int(d**0.5) + 1):
        if d % i == 0:
            divs.append(i)
            if i != d // i:
                divs.append(d//i)
    return sorted(divs)

# Example
a, b = 27, 15
print(divisors(abs(a-b)))  # The result is [1, 2, 3, 4, 6, 12]
```
{% endcode %}

For example $$27 \equiv 15 \bmod n$$ is solved $$n=12$$ because $$27 - 15 = 12$$ and the divisors of $$12$$ are $$\{1,2,3,4,6,12\}$$

* If we use $$4$$ this lets us with $$27 \equiv 15 \bmod 4$$ which is true
* If we use $$6$$ this lets us with $$27 \equiv 15 \bmod 6$$ which is also true
* And so on with any divisor

***

* To find the value of  $$b$$ in an equation $$a \equiv xb \bmod n$$ where we know the $$x$$ coefficient

{% code overflow="wrap" lineNumbers="true" %}
```python
# 
```
{% endcode %}

### <mark style="color:purple;">Congruence System of Equations</mark>

We

### <mark style="color:purple;">Chinese remainder theorem</mark>

We&#x20;

## <mark style="color:blue;">**Modular Inverse**</mark>

Given:

a⋅a−1≡1(modn)a \cdot a^{-1} \equiv 1 \pmod{n}a⋅a−1≡1(modn)

* The modular inverse of `a` modulo `n` exists **iff** `gcd(a, n) = 1`.
* It can be found using the **Extended Euclidean Algorithm**.
* Example:\
  3−1 mod 11=43^{-1} \bmod 11 = 43−1mod11=4 because 3⋅4=12≡1(mod11)3 \cdot 4 = 12 \equiv 1 \pmod{11}3⋅4=12≡1(mod11)

This operation is **crucial for decrypting messages in RSA**.

```
def modinv(a, m):
    gcd, x, _ = extended_gcd(a, m)
    if gcd != 1:
        raise Exception("Modular inverse does not exist")
    else:
        return x % m  # Ensure positive inverse

# Example
print(modinv(3, 26))  # Output: 9 → because 3 * 9 ≡ 1 mod 26
```

## <mark style="color:blue;">Euclidean Algorithm</mark>

The **GCD** is the backbone of many fundamental operations in number theory, algebra, and cryptography. The Euclidean algorithm allows you to calculate it **much faster** than brute force methods — especially with large numbers.

***

#### 🔸 Main Uses of the Euclidean Algorithm:

1. **Find GCD(a, b)**:\
   Quickly determine the largest integer that divides both aaa and bbb without remainder.
2. **Check Coprimality**:\
   If gcd⁡(a,b)=1\gcd(a, b) = 1gcd(a,b)=1, then aaa and bbb are **coprime** — an essential condition in modular arithmetic and cryptographic key generation.
3.  **Compute Modular Inverses** (Extended Euclidean Algorithm):\
    Solving equations like:

    ax≡1(modm)ax \equiv 1 \pmod{m}ax≡1(modm)

    requires gcd⁡(a,m)=1\gcd(a, m) = 1gcd(a,m)=1, and the Euclidean algorithm is used to compute xxx.
4. **Support for Cryptography**:\
   Algorithms like **RSA** require:
   * Computing GCDs
   * Finding coprime values
   * Deriving modular inverses
5. **Simplifying Fractions**:\
   Reduce ab\frac{a}{b}ba​ to lowest terms by dividing numerator and denominator by their GCD.

***

#### 🧠 Intuition Behind the Algorithm

If a number divides two others, it must also divide their difference.\
So instead of checking all possible divisors, we reduce the problem step by step:

gcd⁡(a,b)=gcd⁡(b,amod  b)\gcd(a, b) = \gcd(b, a \mod b)gcd(a,b)=gcd(b,amodb)

This recursive reduction continues until the remainder is 0. The last non-zero number is the GCD



Here we find a coding implementation:

{% code overflow="wrap" lineNumbers="true" %}
```python
def gcd_euclidean(a, b):
    while b != 0:
        a, b = b, a % b
    return a

def gcd_euclidean_recursive(a, b):    # We can also do it using recursion
    return a if b == 0 else gcd_recursive(b, a % b)
    
print("Enter two numbers to find their GCD:")
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))
print(" The GCD is:", gcd_euclidean(a, b))
```
{% endcode %}

### <mark style="color:purple;">Extended Euclidean Algorithm</mark>

ffff

Here we find a coding implementation:

{% code overflow="wrap" lineNumbers="true" %}
```python
def extended_gcd(a, b): # Or its extended version with a⋅u+b⋅v=gcd(a,b)
    old_r, r = a, b
    old_s, s = 1, 0  # Coefficients for a
    old_t, t = 0, 1  # Coefficients for b

    while r != 0:
        quotient = old_r // r
        old_r, r = r, old_r - quotient * r
        old_s, s = s, old_s - quotient * s
        old_t, t = t, old_t - quotient * t

    # old_r is gcd, old_s is u, old_t is v
    return old_r, old_s, old_t

print("Enter two numbers to find their GCD:")
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))   
gcd, u, v = extended_gcd(a, b)
print(f"The GCD is:{extended_gcd(a, b)}")
print(f"The Bezout Identity is {a}*{u} + {b}*{v} = {gcd}")
```
{% endcode %}
