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

# Command Operators

* Execute a command and run it in background

{% code overflow="wrap" lineNumbers="true" %}
```bash
$command &
```
{% endcode %}

***

* Execute a list of commands

{% code overflow="wrap" lineNumbers="true" %}
```bash
$command1 && $command2
```
{% endcode %}

{% hint style="info" %}
**Note:** The next command only will be executed if previous was successful
{% endhint %}

***

* Redirects the output of a command to a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
$command > $filename
```
{% endcode %}

{% hint style="info" %}
**Note:** If file doesn't exit it will be created, and if it exists it will be overwrited
{% endhint %}

***

* Redirects the output of a command to a file but it appends it to the final, don't overwrite it

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>$command >> $filename
</strong></code></pre>

***

* Tooks content from a file

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>$command &#x3C; $filename
</strong></code></pre>

***

* Pass the result of a commnad as parameter for the other

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>$command1 | $command2
</strong></code></pre>

***

* Cath an error into a file

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>$command1 2>$filename
</strong></code></pre>

{% hint style="info" %}
&#x20;**Note:** The number `2` indicates the `STDERR`
{% endhint %}

***

