---
coverY: 0
---

# Release v2.5

### What's new in the release

* Introducing **Thin Teleport**, this feature allows users to teleport a volume to a remote ionir cluster and only copy blocks on-demand, without background sync. This feature is aimed for use cases where only partial data is required by design, and in egress cost sensitive setups.
* **Clone while Teleporting** feature allows users to create clones of a volumes while it is being teleported from another cluster. This feature is aimed at rapid deployments use cases where scale and agility are key.
* New option added for **log collection** including time scoping and logs/metrics only options.
* A new storageclass out of the box support for 8k block-sized volumes
* Starting version 2.5, administrators can control the deployment of ionir pods and services to specific nodes within a cluster – also referred as **Role based Install**.
* Tech Preview – Performance Optimized storageclass, thick provisioning.

### Known Issues

*   **Issue**: Kubernetes clusters’ upgrades or node draining/cordon take significantly longer.\
    **Details:** This happens since once a node is down Ionir rebuilds the resiliency of the data in case of node failure.\
    **Workaround:** Plan longer upgrade cycles and nodes draining time


* **Issue**: Prometheus might display non-consecutive time caused by node crashing.\
  **Details:** This happens since Prometheus is using a persistent volume which is locked by Kubernetes for protection and by-design. In addition, Prometheus rebuild its DB as part of node recovery.\
  **Workaround:** None.
* **Issue**: Nested Teleport is not supported.\
  **Details:** While a volume is being Teleported the destination volume cannot be cloned or Teleported until the preceding Teleport is done successfully.\
  **Workaround:** Allow the initial Teleport to complete before initiating an additional one.
* **Issue**: Volumes **** and clones created do not have any history kept.\
  **Details:** Failing to define historyPolicy parameter within the storageClass YAML will result in default value (0s) – no history will be saved for that storageClass.\
  **Workaround:** Define your desired policies prior to deployment, default values can be updated.
* **Issue**: In case of a component failure that triggers a rebuild, the system might show redundancy issues for an extended period.\
  **Details:** If while data rebuilding operations the cluster is scaled (additional nodes added) this impacts the system’s perception of healthy.\
  **Workaround:**  Allow rebuilding operation to finish prior to scaling the cluster.\


****

****

****

****

****

