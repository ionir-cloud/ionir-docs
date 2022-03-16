# Worker Nodes Requirements

Ionir Data system requires the following to be fully performant and production-ready.

* 8 vCPUs (Cores)
* 32GB of RAM
* local NVMe Drives
* Single Network Interfaces
* Boot Disk of at least 50GB

{% hint style="info" %}
These requirements are for **Ionir Platform only**. Allow additional resources capacity to run your application as you see fit.\
\
This should not be the specification of the entire cluster.
{% endhint %}

### Supported Worker Operating System

Supported OS images as part of OCP compatibility per-version:

* Red Hat Enterprise Linux CoreOS (RHCOS)

### **Total Physical Capacity Requirements**

The following minimum physical capacity is required for a Ionir installation. The minimum cluster size is determined by the minimum number of Ionir nodes that have media **installed locally.** This is the sum of capacities of all NVMe devices that can be used by Ionir across all nodes of the K8s cluster.

* For a 3-node deployment cluster total of 3.6 TB
