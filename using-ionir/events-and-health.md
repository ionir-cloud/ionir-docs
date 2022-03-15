# Events and Health

## **Events Screen**

Ionir displays the main events in each cluster. Events are collected and analyzed using leading log collections and analytics solutions that are part of the Ionir installation.

Elastic ELK stack ([https://www.elastic.co/elk-stack](https://www.elastic.co/elk-stack)) is used to collect, store and analyze the logs to generate system events and alerts.

To view the cluster events in the Ionir Cloud Manager UI, open the UI in the web browser, select the cluster and click **Events**.

![](<../.gitbook/assets/Screen Shot 2022-03-15 at 17.54.45.png>)

Sort the events by clicking the title of the column. Use the “Search” to find and filter for specific events. Multiple values can be used.

There are four (4) event types:

* **Information** - Events related to routine successful system operations. Examples: volume created, node added, volume deleted.
* **Warning** - Events the user should be aware of, but do not require immediate action. Examples: capacity over a specific threshold, pod crashed.
* **Error** - Events about failed operations. Retry the operation.
* **Critical** - Events that require immediate user intervention. Examples: usage over the critical capacity threshold.

## Cluster Health

Cluster health can be one of the following three (3) options:

![](<../.gitbook/assets/Screen Shot 2022-03-06 at 20.35.37 (1).png>)

Hovering over a yellow or red indicator displays the events or errors that are causing the issue.

Here are the reasons that may cause the cluster health to be warning (yellow) and the actions that are required to fix them. Alert indicator needs to be acknowledged post fix to return to green.

| Reason                                                                                                        | Action                                                                                  |
| ------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| One or more of the media devices failed                                                                       | Replace the missing media device.                                                       |
| Some data does not have full redundancy (can happen after media device or node failure)                       | No action needed - Ionir rebuilds the redundancy using other media devices              |
| System is low on capacity                                                                                     | Delete data or volumes that are not required.                                           |
| Ionir is unable to monitor the cluster health status (for example: unable to get node status from Kubernetes) | <p>Verify that Kubernetes is running properly.<br>Verify that all pods are running.</p> |

Here are the reasons that may cause the cluster health to be Error (Red) and what to do in case of each error:

| **Reason**                   | Action                                                            |
| ---------------------------- | ----------------------------------------------------------------- |
| A critical Ionir pod is down | <p>Check that all Ionir pods are running.<br>Contact support.</p> |
| Ionir failed to read data    | Contact support.                                                  |

{% hint style="danger" %}
The system will go into read-only mode once it reaches 100% capacity. The system will go into read-write mode (normal operations) once capacity drops below 98%. The application needs to be reconfigured accordingly.
{% endhint %}
