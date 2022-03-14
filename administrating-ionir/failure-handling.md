# Failure Handling

### Ionir Failure Domains

Ionir failure domain is a node (server) with at least one (1) NVMe media device. This means that copies of the data (used for data redundancy), will always be stored on **different** nodes, even if a node has multiple media devices.

### Media Device Failure

Ionir data resilience is achieved using 3-way mirroring. This protects against two (2) media devices failure. In case of a media device failure, Ionir rebuild process will start automatically and create redundant copies until the desired redundancy level is achieved (3 copies).

{% hint style="info" %}
Clusters that have less than 5 compatible nodes (failure domains), only support a **single** node (failure domain) failure. This is since ETCD is deployed with only three (3) copies and will lose consensus if more than one node fails.
{% endhint %}

### Cluster Status and Events

When a media device fails, an event will be triggered in Ionir showing the media device failure and the serial number of the media device.

In the case of one or multiple media device failure, the system status (health indicator) will turn <mark style="color:yellow;">YELLOW</mark>.

If there is not enough capacity or failure domains available in the cluster to create **at least** two copies of the data, the system status (health indicator) will turn <mark style="color:red;">RED.</mark>

{% hint style="info" %}
To find the node name of the failed media device, run the following command:

`kubectl -n ionir describe mediaresources.crd.ionir.com`

This lists the information of all the media devices used by Ionir.
{% endhint %}

### Acknowledge Media Failures

In version 2.6, when a media device fails or is removed from one of the nodes of the cluster the cluster health indicator shows the event and on top of that an additional “Acknowledge Media Failures” icon is displayed next to it. To clear ALL media errors, click the “Acknowledge Media Failures”.

This option is available since Ionir monitors all the media devices in the cluster and their serial number. In case a media device is removed or fails, Ionir identifies it and triggers the alert. Replacing the media device with another media device (with a different serial number) does not clear the alert. In these cases, the only way to clear the alert is to click the _“Acknowledge Media Failures”_ icon. If a media device is removed and then is placed back, the alert is cleared automatically.

### Node Failure

Node failure reduces the resources that are available in the cluster.

In case of a compute only node (did not have any media devices used by Ionir), some performance degradation might occur (depends on cluster size remaining resources etc). <mark style="color:red;"></mark> In case the failed node has media device/s that were used by Ionir, Ionir will rebuild the data on other nodes in the cluster (see Media Device Failure).

### Cluster Status and Events

In the current version cluster status is derived only from the media devices and pods status. If a node fails, the cluster status will be derived from the media devices that were on the node and from the pods that need to be rescheduled to other nodes.

### ETCD Considerations

Ionir configurations are stored on an internal [ETCD](https://etcd.io), a key-value database that is installed and managed by Ionir. Each copy of the ETCD is running in a different failure domain.  ETCD database requires a [consensus](https://blog.containership.io/etcd/) (majority) of the members to work properly.

Ionir can be deployed using five (5) or three (3) copies of the ETCD database. Kubernetes cluster that has less than five (5) compatible nodes, can only sustain a single node failure. Clusters with five (5) or more compatible nodes, can sustain two nodes failure.

In case ETCD does not have a consensus, Ionir I/O operations will stop until the majority of the ETCD instances are running.

{% hint style="info" %}
Currently, **** There is no option to change the number of ETCD copies once Ionir is installed
{% endhint %}

### UI Considerations

Ionir UI (Dashboard) is managed by a microservice pod in the system named _ionir-ui_. In some cases where there is a crash of worker node running this pod, and there are LB or/and proxy handling the HTTPs connections, a refresh is required to return to full operation. This is an expected behavior.

### Cluster Health

Cluster health can be one of the following three (3) options:

![](<../.gitbook/assets/Screen Shot 2022-03-06 at 20.35.37.png>)

Hovering over a yellow or red indicator displays the events or errors that are causing the issue.

Here are the reasons that may cause the cluster health to be warning (yellow) and the actions that are required to fix them:



| **Reason**                                                                                                    | **Action**                                                                             |
| ------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| One or more of the media devices failed                                                                       | Replace the missing media device                                                       |
| Some data does not have full redundancy (can happen after media device or node failure)                       | No action needed - Ionir rebuilds the redundancy using other media devices             |
| System is low on capacity                                                                                     | Delete data or volumes that are not required                                           |
| Ionir is unable to monitor the cluster health status (for example: unable to get node status from Kubernetes) | <p>Verify that Kubernetes is running properly.<br>Verify that all pods are running</p> |

Here are the reasons that may cause the cluster health to be Error (Red) and what to do in case of each error:



| **Reason**                   | **Action**                                                      |
| ---------------------------- | --------------------------------------------------------------- |
| A critical Ionir pod is down | <p>Check that all Ionir pods are running<br>Contact support</p> |
| Ionir failed to read data    | Contact support                                                 |

