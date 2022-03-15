# Environment Settings

It is recommended to change the value of the following Kubernetes parameters to these recommended values. Changing the values will help Kubernetes to respond faster to different failures:

| Kubernetes         | Parameter Name               | Default | Recommended |
| ------------------ | ---------------------------- | ------- | ----------- |
| kube-apiserver     | events-ttl                   | 1hr     | 72hrs       |
| kubelet            | node-status-update-frequency | 10s     | 5s          |
| controller-manager | node-monitor-period          | 5s      | 2s          |
| controller-manager | node-monitor-grace-period    | 40s     | 15s         |
| controller-manager | pod-eviction-timeout         | 5m      | 30s         |

### Audit Logs <a href="#_heading-h.2s8eyo1" id="_heading-h.2s8eyo1"></a>

It is highly recommended to enable [Kubernetes Audit logs](https://kubernetes.io/docs/tasks/debug-application-cluster/audit/). Enabling the logs provides better visibility to cluster events and provides a better understanding of different issues that may occur in the cluster. Example can be found on [https://github.com/ionir-cloud/ionir-labs](https://github.com/ionir-cloud/ionir-labs)

### Cluster Size <a href="#_heading-h.17dp8vu" id="_heading-h.17dp8vu"></a>

Ionir supports a minimum of five (5) worker nodes for production deployments and three (3) for evaluation deployments. Evaluation deployments with three nodes do not support dual-node failure and cannot be upgraded to support production deployments.
