# Volume Teleport Operation

## Teleporting a Volume

Ionir Teleport (instant mobility) feature provides a unique way to instantly copy a volume between clusters. Less than a minute after the operation is triggered, the volume becomes available in the destination cluster and can be used for read and write operations.

The Teleport operation requires that the source and destination clusters be part of the same Ionir Cloud. While Teleport is performed the clusters must remain peered to allow proper communication.

For information about how to connect clusters, refer to the _“Connecting Clusters”_ section in the _Ionir Administrator Guide_.

**To teleport a volume:**

****

1. Open the Volumes view and select the source volume.
2. The data teleport operation can be initiated from the context menu next to the volume,\
   select **Teleport.**
3. Select the destination **Cluster.**
4. Select the destination **History Policy**. For information about History Policies, refer to the [History Policy](../ionir-admin-guide/storageclass-and-historypolicies.md#creating-a-history-policy) section.
5. Provide the destination **Volume name** (PVC) – The default name is the same as the source PVC. \
   If a PVC with the same name in the selected namespace already exists in the destination cluster, the operation will fail.
6. &#x20;Select the destination **Namespace** from the dropdown list.
7. Toggle for Thin Teleport option, if required.
8. Click **Teleport**.

{% hint style="warning" %}
A storageclass with the same name and parameters must exist on the destination cluster prior to Teleport.
{% endhint %}

{% hint style="warning" %}
The teleport operation creates a PV and PVC. The PVC is created in the selected namespace.
{% endhint %}

<\<IMAGE>>

Click **GO TO DESTINATION** to open the destination cluster dashboard or click **Close** to go back to the current view.

## Volumes Status

The volume shows up in the destination cluster. During the teleport operation, the destination volume goes through three stages (states):

1. **Initializing** – The volume’s metadata is being transferred. During this stage the destination volume cannot be used. This stage usually takes less than a minute.
2. **Accessible** – Once the metadata copy completes, the volume’s data will be transferred. During this stage, the volume is fully accessible for "read and write" operations, regardless of the volume size. Thanks to Ionir’s deduplication, only unique, compressed, new blocks are copied, reducing the bandwidth consumption. If the volume disconnects from the source volume for any reason it will remain in its current state.
3. **Available** – Once the copy of all the volume data completes the status of the volume will become Available. At this point, the connection to the source volume is not required and the volume is available just like any other volume.

{% hint style="success" %}
Once the volume is in the _“Accessible”_ state (2nd stage), it can be allocated to a pod that can read and write data to the volume.
{% endhint %}

## Cancelling Teleport Operation

During a data teleport operation, while the status of the destination volume is _“Accessible”_ the destination volume pulls data from the source volume. To stop the teleport operation, delete the volume (PVC) on the destination cluster using the kubectl delete command.

## Deleting the Source Volume During Teleport

While teleport is in progress the source volume should not be deleted. Deleting the source volume (PV) will cause additional capacity consumption on the source cluster.

While teleporting is in progress, trying to delete the source PVC of the source volume will not delete the PV of the volume even if the Reclaim Policy is set to “Delete”. This is a protection mechanism to prevent the deletion of the resource that is in use. If the PVC has been deleted, **wait for the teleport operation to complete,** and manually delete the PV of the volume.

#### **Teleport Progress and Statistics** <a href="#_toc87788806" id="_toc87788806"></a>

Volume data teleport progress and statistics can be viewed on the destination cluster.

**Teleport Progress**

To view the data teleport progress, open the destination cluster and find the volume that is being teleported. Once the volume is in _“Accessible”_ mode hover over the progress icon to view the progress.

**Teleport Statistics**

To monitor the teleport statistics that includes the total data teleported to the cluster and the incoming teleport throughput open the dashboard manually by clicking _“Open in Grafana”_ and selecting the _“Cluster Teleport Statistics”_ dashboard.
