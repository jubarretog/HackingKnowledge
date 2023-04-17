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



* Redirects the output of a command to a file but it appends it to the final, don't overwrite it

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>$command >> $filename
</strong></code></pre>
