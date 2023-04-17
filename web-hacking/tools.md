# Tools

## <mark style="color:green;">Steghide</mark>

### **Characteristics:**

* Stenography Program

### **Comands:**

* Install

{% code overflow="wrap" lineNumbers="true" %}
```bash
sudo apt-get install steghide
```
{% endcode %}

***

* Shows embedded information got from a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
steghide info $filename
```
{% endcode %}

***

* Extract embedded data from a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
steghide extract -sf $filename
```
{% endcode %}

{% hint style="info" %}
**Note:** Flag `-sf` specifies to get information from a stego file
{% endhint %}



## <mark style="color:green;">Burp Suite</mark>

### **Characteristics**

* Digital plattform tha collects tools for specialiced web penetration testing.
* Framework written in Java that aims to provide a one-stop-shop for web application penetration testing
* Capture and manipulate all of the traffic between an attacker and a webserver
* Can intercept, view, and modify request
* Burp suite has modules that can be added

### **Features**

* **Proxy:** Allows us to intercept and modify requests/responses.
  * _Foxy Proxy:_ Browser Extension for using proxy on Burp
  * The standart IP for connection with Burp is 127.0.0.1 on port 8080
* **Repeater:** Allows us to capture, modify, then resend the same request numerous times. We could craft requests by hand too.
* **Intruder:** Allows us to spray an endpoint with requests.
* **Decoder:** Allows us to transform data, decoding captured information, or encoding a payload.
* **Comparer:** Allows us to compare two pieces of data at either word or byte level.
* **Sequencer:** Help us asses random tokens or other generated data.

