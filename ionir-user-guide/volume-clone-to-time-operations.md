# Volume Clone (to Time) Operations

## Creating Clones with Ionir

The Ionir clone operation creates an instant clone of a volume in the same cluster. Thanks to Ionir’s deduplication capability, clone operation does not require additional space until new data is written to them. All clone operations in the system are crash consistent. For application consistency, the application must be quiesced making all changes from the filesystem to be written to disk.

Clones are independent volumes that can be cloned again as needed. There are no dependencies between clones and their source volumes.

Clone to time enables creating an instant clone of a volume in 1-second granularity back in time. This granularity is defined by the history policy setting found in the respective storage class. This clone is fully independent, write-enabled and creating new clones of it is supported based on the assigned storage class.

**To clone a volume:**



1. Open the Volumes view and select the volume.
2. The clone operation can be initiated from the context menu next to the volume,\
   select **Clone**.
3. Provide a name for the clone volume (PVC). The default name of the volume is the original volume name with the unix timestamp.\
   If a PVC with the same name already exists in the selected namespace, the operation will fail.
4. Select the destination **History Policy**. For information about History Policies, refer to the History Policy section.
5. Select the **Namespace** for the clone. By default, the cloned PVC will be created in the same namespace of the source volume (PVC).
6. Select whether you want to **Clone Now** or **Clone To Time**. If you select **Clone To Time**, select the clone time. The **Oldest Available** indicates the oldest clone available.
7. Click **Clone**.

<\<Image>>

The clone operation creates a PV and PVC. The cloned volume is created with the same storage class as the source volume. History Policy and Namespace are configurable.

## Clone Teleported Volume (During Accessible State) <a href="#_toc87788811" id="_toc87788811"></a>

As of version 2.5, it is now supported to clone a volume while it is being teleported from the source cluster. This will create multiple copies in an Accessible state for the duration of teleporting the source volume. After Teleport is complete, all clones will appear as Available.

## Volume Clone Using CSI Volume Cloning Feature

The CSI Volume Cloning feature adds support for specifying existing PVCs in the _data-source_ field to indicate a user would like to clone a Volume. A Clone is defined as a duplicate of an existing Kubernetes Volume that can be consumed as any standard Volume.

Ionir fully supports this feature and adds an additional capabilities on top of the basic volumes cloning parameters. These are listed under _“annotations”_ in the clone YAML file. The following is an example of Ionir-powered cloning YAML:

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
    name: clone-of-pvc-1
    namespace: clone-ns
    annotations:
// <data-source, option a>
      ionir.com/source-pvc-name: pvc-1
      ionir.com/source-pvc-namespace: clone-ns
// <data-source, option b>
      ionir.com/source-pv: pv-1
// <optional>
      ionir.com/source-timestamp: <timestamp-rfc-3339>
// <optional>
      ionir.com/dest-history-policy: <history-policy> 
spec:
  accessModes:
  - ReadWriteOnce
  storageClassName: same_as_parent
  resources:
    requests:
      storage: 5Gi
```

