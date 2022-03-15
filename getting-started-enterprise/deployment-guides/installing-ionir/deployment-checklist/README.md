# Deployment Checklist



### Installation Prerequisites

1. **Installer machine:** Refer to the Installer Machine Requirements section.
2. **Kubernetes/Ionir nodes:** Refer to the _Ionir Deployment Requirements_ document.
3. **kube-system** pods are running and healthy.

### Installation Files

Ionir installer is shipped as a package (tar file). There are three (3) main files for the manual installation of Ionir storage system.

* `ionir.sh` – the actual install script
* `ionir-compatibility-check.sh` – preflight install validation
* `ionir.scaled_cluster.conf`– cluster configuration file

All installation files (tarball content) must reside in the same directory on the installer machine.

### Installer Machine Requirements

* Linux-based machine (virtual or physical)
* Network connectivity to the Kubernetes cluster
* kubectl installed – For information on how to install kubectl, refer to [online resources](https://kubernetes.io/docs/tasks/tools/install-kubectl/).
* KUBECONFIG environment variable configured to the cluster where you would like to install Ionir.

###

###

