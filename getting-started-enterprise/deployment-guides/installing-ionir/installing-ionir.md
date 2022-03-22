# Installing Ionir

{% hint style="warning" %}
**Important**: Before installing Ionir it is required to run the Ionir Compatibility Check Tool to verify the cluster is compliant with all prerequisites.
{% endhint %}

To install Ionir:

1. Open a Linux console and go to the directory with the installation files.
2.  Make sure **KUBECONFIG** is pointing to the right Kubernetes cluster.\
    The installation script expects to get the following parameters: \[Optional]

    ```
    -a 'install', 'uninstall', 'stop', 'start' or 'upgrade' Ionir.
    -k Ionir license key 
    -l accept In order to be able to use the installer, Ionir EULA must be accepted by adding '-l accept' to the command line 
    -f Set ionir.sh configuration file. Note: Ionir scaled configuration requires at least 5 worker nodes. 

    [-r ] Image registry, default is quay.io/ionir 
    [-t ] Image tag, default is latest
    [-u ] Image registry username (required when working with a local registry) 
    [-p ] Image registry password (required when working with a local registry) 
    [-c ] The cert host path for self-signed local registry (for example /etc/docker/certs.d) 
    [-o] Run preflight only for Ionir 'stop', 'start' or 'upgrade' actions 
    [-e ""] Set ionir.sh extra options 
    [-v] Set to run in non-interactive mode 
    [-q] Set -q for quiet mode. By default, the installer logs are directed to the console
    ```
3. Run the **ionir.sh** script to install Ionir:\
   `./ionir.sh -a install -r <registry> -t <tag_name> -f <config_file>  -l accept -k <license key>`

Here is an example where Ionir is installed with aand where the number of nodes is less than 5. In this example, the default registry (**quay.io/ionir**) is used:

`./ionir.sh -a install -f ionir.min_cluster.conf -l accept -k <license key>`

Below is an example that specifies the registry location:

`./ionir.sh -a install -r 172.17.1.1 -f ionir.min_cluster.conf -l accept -k <license key>`

Ionir installer pulls the images from the repositories and deploys Ionir on the cluster.

### Role`-`Based Install

Starting version 2.5, administrators can control the deployment of ionir pods and services to specific nodes within a cluster – also referred as Role-based Install.

This is achieved using Node Affinity – a basic Kubernetes concept. Node affinity is a property of Pods that attracts them to a set of nodes. Taints are the opposite -- they allow a node to repel a set of pods.

To enable this install feature, administrators are required to these two steps

#### Step 1:

Add labels to the designated nodes for ionir by using the following command:

`kubectl label nodes <node_name> ionir.com/role-all=true`

#### Step 2:

Add the following flag “--hetero-install” to the installation command, for example:

`./ionir.sh -a install -f <config_file> --hetero-install -l accept -k <license key>`

{% hint style="info" %}
Role-based deployment is controlling only ionir system environment (and namespace), ionir-installer does not share this option and can run anywhere.
{% endhint %}

### Installation Progress

The installation logs are displayed in the installation shell or you can view the logs of the **ionir-installer-**_**\<id>**_** pod** that runs under the **ionir-installer** namespace by running the following command:

`kubectl -n ionir-installer logs ionir-installer-`_`<id>`_

{% hint style="info" %}
Post-installation local disks (media) and local NIC will be managed by ionir in userspace and will not appear under the node OS control. `lsblk/ifconfig` will not list these resources.
{% endhint %}

### Reinstalling Ionir

In case there is a need to reinstall Ionir, rerun the Ionir installation command as described in Installing Ionir. This uninstalls and reinstalls Ionir on the cluster.

{% hint style="warning" %}
&#x20;If there are any volumes (PV) in the cluster that use Ionir as the provisioner, the operation might fail.
{% endhint %}

### Uninstalling Ionir

Uninstalling Ionir removes all components that were installed by Ionir from the cluster.

{% hint style="info" %}
Before uninstalling Ionir make sure there are no volumes (PVs) in the cluster that use Ionir as the provisioner. If Ionir volumes exist in the cluster, the uninstall will fail.
{% endhint %}

To uninstall Ionir:

1. Open a Linux console and go to the directory with the installation files.
2. Make sure **KUBECONFIG** is pointing to the right Kubernetes cluster.
3. Run the following command:\
   `ionir.sh -a uninstall -f <config file>`_`-k <license key>`_&#x20;

The uninstall log is displayed in the shell or you can view the logs of the **Ionir-installer** pod that runs under the **Ionir-installer** namespace by running the following command:

`kubectl -n ionir-installer logs ionir-installer-`_`<registry id>`_
