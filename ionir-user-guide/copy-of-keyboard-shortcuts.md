# Introduction

Ionir is a container-native data platform for Kubernetes. Ionir virtualizes all available storage in a Kubernetes cluster to create a single pool of highly scalable storage. Having a Container Storage Interface (CSI) plugin, Ionir storage can be provisioned and managed by Kubernetes, the common control plane in the environment.

In addition to providing resilient, high-performance storage, Ionir also provides end-to-end data management capabilities. The Ionir architecture separates the metadata from the data, which enables unique data management capabilities such as instant clones. The microservices architecture provides a unified data platform that is elastic, scalable, and agile, which is critical for containerized deployments.

### Deployments vs Statefulsets

**Deployments** are usually used for stateless applications. However, you can save the state of deployment by attaching a Persistent Volume to it and making it stateful, but all the pods of a deployment will be sharing the same Volume and data across all of them will be the same.

**StatefulSet** is also a Controller but unlike Deployments, it doesn’t create ReplicaSet rather it creates the Pod with a unique naming convention. e.g. If you create a StatefulSet with a name counter, it will create a pod with the name counter-0, and for multiple replicas of a statefulset, their names will increment like counter-0, counter-1, counter-2, etc

Every replica of a stateful set will have its own state, and each of the pods will be creating its own PVC (Persistent Volume Claim). So a statefulset with 3 replicas will create 3 pods, each having its own Volume, so total of 3 PVCs. It is a best practice to use statefulsets when persistency is required.

Ionir creates volumes corresponding to PVCs and supplies a correspondent PV to it. Raw volume supported size is 1 PiB, EXT4/XFS volume size is 16TB.&#x20;
