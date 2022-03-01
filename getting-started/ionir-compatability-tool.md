# Ionir Compatability Tool

The compatibility check tool can run on any Linux machine that has kubectl[ ](https://kubernetes.io/docs/tasks/tools/install-kubectl/)[installed](https://kubernetes.io/docs/tasks/tools/install-kubectl/) and has a directory with the compatibility tool script and yaml files. A namespace called “ionir-compatibility-check” is created and will be deployed with a pod on each node (using daemonset) in the namespace.

**To run the compatibility Check Tool, follow these steps:**

1. Open the compatibility check directory in a Linux console.
2. Make sure kubectl is installed and that KUBECONFIG is configured to the kubernetes cluster
3. The compatibility check script expects to get the following parameters:

```
-i  : Install compatibility tool
-r  : [optional] image registry to pull the images from (default: quay.io/ionir)
-u  : username for the image registry
-p  : image registry password
-t  : image tag name
-s  : [installation type] Ionir's installation type, may be either 'minimal', for up to 4 nodes or 'scale', for a larger clusters
```

Run the `ionir-compatibility-check.sh` script to install the tool:

```
ionir-compatibility-check.sh -i -r <registry> -u <user> -p <password> -s [install type] -t <tag>
```

For example on running the tool with user “ionir” and password “test” and size “minimal” using default quay.io/ionir public repo:

```
./ionir-compatibility-check.sh -i -u ionir -p test -s minimal -t v2.4
```

The test will verify that all nodes meet the minimal hardware and software requirements, that the cluster network meets Ionir requirements, and those images can be pulled from the image registry.

**Overall Result** - The first section in the result is the overview status of the cluster. The following output indicates that the Kubernetes cluster is correctly configured for a successful Ionir installation. You need to stop the script manually.

{% hint style="info" %}
&#x20;If any other result is shown, please contact technical support [support@ionir.com](mailto:support@ionir.com)
{% endhint %}
