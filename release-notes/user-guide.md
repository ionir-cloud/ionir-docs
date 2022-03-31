# Release v2.6



### What's new in the release

* Faster Rebuilding Times
* New OCP versions support 4.8/4.9
* Community License Available

### Known Issues

* **Issue**: Volumes Status reports "Available" during teleport even during network disconnect.\
  **Details:** While Teleporting a volume between clusters a **live** network connection is required in order to present data from source to target, on-demand or background sync. Currently, a network disconnection is not reflected in volumes status, although new data can't be served.\
  **Workaround:** No Workaround.
* **Issue**: Kubernetes clusters’ upgrades or node draining/cordon take significantly longer. This includes Pod Disruption Budgets warnings on OCP platforms.\
  **Details:** This happens since once a node is down Ionir rebuilds the resiliency of the data in case of node failure.\
  **Workaround:** Plan longer upgrade cycles and nodes draining time
* **Issue**: Prometheus might display non-consecutive time caused by node crashing.\
  **Details:** This happens since Prometheus is using a persistent volume that is locked by Kubernetes for protection and by design. In addition, Prometheus rebuild its DB as part of node recovery.\
  **Workaround:** None.
* **Issue**: Nested Teleport is not supported.\
  **Details:** While a volume is being Teleported the destination volume cannot be cloned or Teleported until the preceding Teleport is done successfully.\
  **Workaround:** Allow the initial Teleport to be completed before initiating an additional one.
* **Issue**: Volumes **** and clones created do not have any history kept.\
  **Details:** Failing to define historyPolicy parameter within the storageClass YAML will result in default value (0s) – no history will be saved for that storageClass.\
  **Workaround:** Define your desired policies prior to deployment, default values can be updated.
* **Issue**: In case of a component failure that triggers a rebuild, the system might show redundancy issues for an extended period.\
  **Details:** If while data rebuilding operations the cluster is scaled (additional nodes added) this impacts the system’s perception of healthy.\
  **Workaround:**  Allow rebuilding operation to finish prior to scaling the cluster.
