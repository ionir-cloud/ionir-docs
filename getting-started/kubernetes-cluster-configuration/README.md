# Kubernetes Cluster Configuration

Ionir aggregates the capacity and performance of **local NVMe SSDs** on the worker nodes of the Kubernetes cluster and provides a distributed storage layer to all nodes in the cluster. Only one Ionir cluster per Kubernetes cluster can be configured.

A minimal **production configuration requires at least five (5) worker nodes** (failure domains) in the Kubernetes cluster with at least one NVMe drive per node. Such a configuration protects against a failure in 2 separate failure domains which is the recommended minimum for production environments.

For non-production clusters a minimum of 3 worker nodes for use as PoC or test environment, but such configurations cannot be converted later to production use and are not resilient to two failures.

It is recommended that all nodes will have the same media configurations and homogeneous as possible.&#x20;
