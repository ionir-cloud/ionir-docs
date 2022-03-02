# Networking Requirements

### Load-Balancer Services

An external load balancer (such as [MetalLB](https://metallb.universe.tf)) is required on the Kubernetes cluster to provide an externally accessible IP address for the Ionir platform in general and mobility between cluster specifically. This Load-balancer resource should be configurable at the Kubernetes level using standard services.

{% hint style="info" %}
Example MetalLB deployment YAML can be found on ionir GitHub repository [here](https://github.com/ionir-cloud/ionir-labs/).
{% endhint %}

### Networking Requirements

Ionir creates a high performance dedicated virtual network for storage traffic, and hence requires that the underlying network infrastructure provide sufficient performance:

* For production environments network speed must be 25 Gb or higher. 10 Gb may be used in non-production environments.
* SR-IOV must be enabled on the NIC as best practice. Optionally use multiple physical adapters if applicable.
* Full IP connectivity is required between all nodes **in the cluster**.
* Full IP connectivity is required between all nodes **between clusters for mobility.**

### Datapath Network Configuration

Ionir creates a dedicated high-speed data network between all worker nodes in the cluster. This network is used for communication between the Ionir system pods and provides ahigh-performance data-path.

This network can be virtual using the same physical interface as that used by Kubernetes by enabling SR-IOV on the network adapters, or it can be configured using dedicated NICs.

{% hint style="info" %}
**Note:** Ionir datapath network must be configured with a unique subnet. This network does not require a default gateway and is internal only.
{% endhint %}

The following configuration is required for each worker node in the cluster:

* Set a second **static IP** for the node on the interface for the data path network (physical or virtual function). This datapath IP must be part of the datapath subnet.
* MTU should be set to 9000 or higher (Jumbo frames).
* In addition, you must configure Kubernetes CNI (for example Calico) to use the public network NIC only (not the dedicated mentioned) for general cluster communications. Further examples are listed here:[ https://docs.projectcalico.org/networking/ip-autodetection](https://docs.projectcalico.org/networking/ip-autodetection)
* &#x20;Kubernetes label must be set that states the datapath IP of the node must be added to **each worker node**. To set the label run the following command for each worker node: \
  `kubectl label node <workerNodeName> datapath_ni=<NodeDatapathIP>`

### Access to Public Registries

Prior to installation contact sales support to get _**quay.io/ionir**_ username and password.

All nodes require direct access to an image registry (either private or public) to be able to pull the Ionir images and other 3rd party images.

Additional public repositories are required as follows:

* quay.io
* Docker.elastic.co
* Docker.io
* k8s.gcr.io

#### **Air gapped environments (no internet connectivity)**

{% hint style="info" %}
A private registry is expected to be found and configured in the customer environment and Docker runtime is required proxy endpoint to successfully run import/export script


{% endhint %}

On an internet connected endpoint run the following script: `images_pull_push.sh`

```
./images_pull_push.sh pull <image list file> <ionir public registry username> <ionir public registry password>
```

Once connected to the private network and validated connectivity to the private registry, run the following:

```
./images_pull_push.sh push image_list.txt <local registry IP> <local registry username> <local registry password>image_list.txt
```

{% hint style="info" %}
image\_list.txt file is part of the installation bundle
{% endhint %}
