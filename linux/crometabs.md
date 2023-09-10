# Crometabs

Special files with formatting that is recognised by the `cron` process to execute each line step-by-step in a regular time

* _MIN:_ What minute to execute at
* _HOUR:_ What hour to execute at
* _DOM:_ What day of the month to execute at
* _MON:_ What month of the year to execute at
* _DOW:_ What day of the week to execute at
* _CMD:_ The actual command that will be executed.

{% code overflow="wrap" lineNumbers="true" %}
```bash
$MIN $HOUR $DOM $MON $DOW $COM   #Example below
0 12 * * * cp -R /home/cmnatic/Documents /var/backups/ #Every 12 hours
```
{% endcode %}

{% hint style="info" %}
**Note:** The<mark style="color:orange;">`*`</mark>let skip the specification of values
{% endhint %}

***

