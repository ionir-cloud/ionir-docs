# Worker Nodes

Ionir&#x20;

### Supported Worker Operating System&#x20;

Supported OS images are:

* RHEL 8.3 / RHCOS 3.11
* CentOS 8.3&#x20;
* Ubuntu 20.04.1 LTS
* SLES15SP2
* Debian 10

{% hint style="info" %}
If you require a different OS please contact ionir support. In general, any distribution of Linux with Kernel 5.0 and above can be used.
{% endhint %}

### Installing Extra-Modules is required on each Linux OS

Ionir requires some extra modules that are might not be part of the upstream kernel. To install these modules please run the following command:&#x20;

```
sudo apt install linux-modules-extra-$(uname -r)
```

### **Physical Capacity Requirements**

The following minimum physical capacity is required for a Ionir installation. The minimum cluster size is determined by the minimum number of Ionir nodes that have media **installed locally.** This is the sum of capacities of all NVMe devices that can be used by Ionir across all nodes of the K8s cluster.

* For a 3-node deployment - 3.6 TB
* For a 5-node deployment and higher - 6TB
