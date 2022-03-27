# Networking Requirements

### Load-Balancer Services

Ionir requires two (2) publicly facing IP addresses as part of the LoadBalancer services/routes deployment, these should be enabled and configured correctly.

### Networking Requirements

Ionir creates a high performance dedicated virtual network for storage traffic, and hence requires that the underlying network infrastructure provide sufficient performance:

* For production environments network speed must be 25 Gb or higher. 10 Gb may be used in non-production environments.
* Full IP connectivity is required between all nodes **within the cluster**.
* External Access to the Ionir Dashboard UI requires ports - 80/443.
* IP connectivity required between all nodes **between clusters for mobility -** 1601/2379.

### Access to Public Registries

Prior to installation contact sales support to get _**quay.io/ionir**_ username and password.

All nodes require direct access to an image registry (either private or public) to be able to pull the Ionir images and other 3rd party images.

Additional public repositories are required as follows:

* quay.io
* Docker.elastic.co
* Docker.io
* k8s.gcr.io

### **Air-Gapped Environments**

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
image\_list.txt file is part of the installation bundle or per request from ionir support
{% endhint %}
