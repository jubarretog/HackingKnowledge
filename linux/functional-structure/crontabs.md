# Crontabs

The **Crontabs** are special files with formatting that are recognized by the _cron_ process to execute each line step-by-step at a regular time. They can be broken down as follows:

* _**MIN:**_ What minute to execute at
* _**HOUR:**_ What hour to execute at
* _**DOM:**_ What day of the month to execute at
* _**MON:**_ What month of the year to execute at
* _**DOW:**_ What day of the week to execute at
* _**CMD:**_ The actual command that will be executed

{% code overflow="wrap" lineNumbers="true" %}
```bash
$MIN $HOUR $DOM $MON $DOW $COM   #Example below
0 12 * * * cp -R /home/$user/Documents /var/backups/ #Do backup every 12 hours
```
{% endcode %}

{% hint style="info" %}
The `*` is used to skip specific values
{% endhint %}
