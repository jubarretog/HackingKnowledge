# Operators

The **Command Operators** allow users to control the flow of commands and processes in the terminal, offering greater flexibility and efficiency. Here is an explanation of their use:

* Execute a command and send it to the background

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
$command1 ; $command2
```
{% endcode %}

{% hint style="info" %}
When using `&&` the next command will only be executed if the previous one was successful
{% endhint %}

***

* Redirects the output of a command to a file

{% code overflow="wrap" lineNumbers="true" %}
```bash
$command > $filename
```
{% endcode %}

{% hint style="info" %}
If the file doesn't exist, it will be created, and if it exists, it will be overwritten
{% endhint %}

***

* Redirects the output of a command to a file, but it appends it to the final instead of overwriting it

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>$command >> $filename
</strong></code></pre>

***

* Takes content from a file

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>$command &#x3C; $filename
</strong></code></pre>

***

* Takes content from a stream

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>$command &#x3C;&#x3C; $stream #Ex: cat &#x3C;&#x3C; EOF   
</strong></code></pre>

***

* Pass the result of a command as a parameter to another command

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>$command1 | $command2
</strong></code></pre>

***

* Catch an error in a file

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>$command1 2>$filename
</strong></code></pre>

{% hint style="info" %}
The number `2` indicates the `STDERR`. A common use is `2>/dev/null` to discard any error
{% endhint %}
