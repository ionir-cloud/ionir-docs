# StorageClass and HistoryPolicy

### Creating a Storage Class

Ionir supports the creation of new storage classes to optimize the volume performance for different applications. To create a new storage class, refer to Kubernetes StorageClass documentation:

[https://kubernetes.io/docs/concepts/storage/storage-classes/](https://kubernetes.io/docs/concepts/storage/storage-classes/)

Ionir storage class requires the following to be defined in the storage class:

* **provisioner**: Determines what volume plugin is used for provisioning the PV. For Ionir this needs to be set to “ionir”
* **type**: Specify the volume type. Supported types are: “ext4”, “xfs” and “block” (raw block device). If not specified, the default value is “ext4”.
* **blockSize**: Specify the volume block size. Supported sizes are 4k, 8k and 16k. If not specified, the default value is 16k.

Below is a table that describes the valid values for the available storage classes:

| **provisioner**   | ionir                            |     |      |
| ----------------- | -------------------------------- | --- | ---- |
| **type**          | block                            | xfs | ext4 |
| **blockSize**     | 4k / 8k / 16k                    |     |      |
| **historyPolicy** | 1-hour-history / 24-hour-history |     |      |

Below is an example of a YAML file to create a storage class for provisioning volumes formatted as EXT4 filesystem with a block size of 16KB:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: ionir-xfs-ext4
provisioner: ionir
```

Below is another example of a YAML to create a storage class for provisioning block volumes with a block size of 4k:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: ionir-xfs-4k
provisioner: ionir
parameters:
  type: xfs
  blockSize: 4k
  historyPolicy: 6-hour-history
```

### Creating a History Policy

The History Policy custom resource definition (CRD) powers the clone to time capability. The History Policy defines the window of time for which Ionir keeps versions of the volume (with 1-second granularity). The volume can then be rolled back to any point in time within that period.

{% hint style="info" %}
The longer the History Policy, the more information is retained, and the more space is required by the backend to maintain the additional copies.
{% endhint %}

The History Policy is defined when the volume is created from the Storageclass. Although Storageclasses are immutable, the History Policy of a volume can be changed after creation.

The following is an example of building a History Policy resource:

```
apiVersion: volume.ionir.com/v1
kind: HistoryPolicy
metadata:
  name: 1-hour-history
  namespace: ionir
spec:
  hoursGranularityRetention: ""
  minutesGranularityRetention: ""
  secondsGranularityRetention: 1h
```

{% hint style="info" %}
The maximum time supported for History Retention is 24hrs. Setting a bigger value will not generate an error.
{% endhint %}
