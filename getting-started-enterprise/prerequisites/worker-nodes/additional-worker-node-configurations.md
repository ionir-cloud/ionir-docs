# Additional Worker Node Configurations

### Additional Modules Required

The following configurations must be prepared prior to installing Ionir:

* Load NVME over TCP module
* Load VFIO - "Virtual Function I/O"
* Configure HugePages

### Using Machine Configuration Operator (MCO) on OCP

All configurations YAML files can be found under ionir GitHub repository [here](https://github.com/ionir-cloud/deployments/tree/main/OpenShift/configuration/machine-configuration-files)

### Manual Configuration

#### NVME/TCP - Run the following commands to add the module:

```
sudo modprobe nvme_tcp
echo 'nvme_tcp' >> /etc/modules-load.d/modules.conf
```

#### VFIO - Run the following to add the module:

```
sudo modprobe vfio_pci
echo 'vfio_pci' >> /etc/modules-load.d/modules.conf
```

{% hint style="info" %}
VFIO kernel is usually present by default in all distributions, however, please consult your distribution's documentation to make sure that is the case.

To determine if VFIO is already in the kernel run: `grep vfio /proc/kallsyms`
{% endhint %}

#### Configure HugePages - Run the following:

```
sysctl -w vm.nr_hugepages=1024
sysctl -p
echo 'vm.nr_hugepages = 1024' >> /etc/sysctl.conf
```

#### Restarting kubelet service is recommended

```
sudo service kubelet restart
```
