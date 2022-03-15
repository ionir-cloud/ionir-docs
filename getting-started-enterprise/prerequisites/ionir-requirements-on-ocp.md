# Ionir Requirements on OCP

### RedHat Openshift Container Platform (OCP) Support

* Support for OCP is through an Operator which will be installed and controls the entire lifecycle of Ionir data platform.
* Ionir version 2.4 and above supports OCP 4.6.x and 4.7.x
* RHCOS as worker nodes OS (for RHEL support contact [support@ionir.com](mailto:support@ionir.com))
* For more information visit RedHat Certified OperatorHub.

#### Ionir Operator <a href="#_heading-h.4bvk7pj" id="_heading-h.4bvk7pj"></a>

Ionir Certified Operator can be found on Openshift OperatorHub, please make sure it is accessible for installation.&#x20;

![](<../../.gitbook/assets/Screen Shot 2022-03-15 at 12.52.46.png>)

### Ionir Machine Configuration

Download and run four (4) machine configuration files examples from [Ionir-cloud GitHub](https://github.com/ionir-cloud/deployments/tree/main/OpenShift/configuration/machine-configuration-files)&#x20;

#### Required Settings - Done using Machine Configuration Operator (MCO) <a href="#_heading-h.1664s55" id="_heading-h.1664s55"></a>

SR-IOV network is an optional feature of an Openshift cluster. To make it work, it requires different components to be provisioned and configured accordingly. For best performance using SR-IOV we recommend that this setting is enabled in the system grub file **on each node**:

* For Intel processors - intel\_iommu must be set to on (intel\_iommu=on) - Example YAML [here](https://github.com/ionir-cloud/deployments/blob/main/OpenShift/configuration/machine-configuration-files/sriov/sriov-mlx-policy.yaml)
* For AMD processors - amd\_iommu must be set to on (amd\_iommu=on)

The following additional modules must be loaded and running examples [here](https://github.com/ionir-cloud/deployments/tree/main/OpenShift/configuration/machine-configuration-files/kernel-modules)

* NVME/TCP - nvme\_tcp (modprobe nvme\_tcp)
* VFIO - vfio-pci (modprobe vfio\_pci)

The following parameters must be tuned as well:

*   2MB hugepages (vm.nr\_hugepages) must be set to 1024 or higher

    Example YAML [here](https://github.com/ionir-cloud/deployments/tree/main/OpenShift/configuration/machine-configuration-files/hugepages)
