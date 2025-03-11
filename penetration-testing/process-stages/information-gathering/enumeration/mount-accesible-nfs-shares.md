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

# Mount accesible NFS Shares

We can mount an NFS being shared over the network if we find an active NFS service running in a target machine.

* Check if exist any NFS share

{% code overflow="wrap" lineNumbers="true" %}
```bash
showmount -e $targetIP
```
{% endcode %}

***

* Create a folder and mount the share under that folder

{% code overflow="wrap" lineNumbers="true" %}
```bash
mkdir $folder
sudo mount -t nfs $targetIP:$folderToMount ./$folder/ -o nolock
```
{% endcode %}

***

* After retrieving the information needed, go back to the initial point and unmount the share

<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>cd $folder/..
</strong><strong>sudo umount ./target-NFS
</strong></code></pre>
