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

# Hypervisors

A **hypervisor** is a software layer or hardware system that allows multiple operating systems to run on a single physical machine by creating and managing virtual machines and even creating virtual network environments between them.&#x20;

<figure><img src="../.gitbook/assets/image (28) (1).png" alt="" width="339"><figcaption></figcaption></figure>

Each virtual machine operates as if it has independent hardware, even though they share the physical resources of the host system.&#x20;

We can find two types of hypervisors:

## <mark style="color:blue;">Type I (</mark><mark style="color:blue;">**Bare-metal**</mark><mark style="color:blue;">)</mark>

* Runs directly on the host’s hardware
* Manages and controls hardware resources like CPU, memory, and storage, and allocates them to the virtual machines
* No underlying operating system is required for it to operate
* Commonly used in data centers and cloud environments due to its efficiency and performance
* Some well-known are [_VMware ESXi_](https://www.vmware.com/products/cloud-infrastructure/esxi-and-esx) and [_Microsoft Hyper-V_](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/)

<figure><img src="../.gitbook/assets/Screenshot_2023-12-18-13-30-18_primary.png" alt=""><figcaption><p><a href="https://www.techtarget.com/searchitoperations/tip/Whats-the-difference-between-Type-1-vs-Type-2-hypervisor">https://www.techtarget.com/searchitoperations/tip/Whats-the-difference-between-Type-1-vs-Type-2-hypervisor</a></p></figcaption></figure>

### <mark style="color:blue;">Type II (Hosted)</mark>

* Software-defined, has another layer of abstraction between hardware and operative system
* Runs on top of a host operating system and the virtual machines run above this hypervisor layer
* The hypervisor relies on the host OS for managing hardware resources
* Some well-known are [_VMware Workstation_](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion) and [_Oracle VirtualBox_](https://www.virtualbox.org/)
* Commonly used for development, testing, or personal virtual machine setups

<figure><img src="../.gitbook/assets/image (17) (1) (1).png" alt=""><figcaption><p><a href="https://www.techtarget.com/searchitoperations/tip/Whats-the-difference-between-Type-1-vs-Type-2-hypervisor">https://www.techtarget.com/searchitoperations/tip/Whats-the-difference-between-Type-1-vs-Type-2-hypervisor</a></p></figcaption></figure>
