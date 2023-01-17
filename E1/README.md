# Setup Kubernetes Cluster with kubeAdm on Linux

My setup contain two servers. One as control plane machine node and the other one as a worker node to be used for running containerized workloads. You can add more nodes to suit your desired use case, load, and HA.

| Role |	Hostname |	Specs |
| --- | --- | --- |
| Master  |	master01.techinet.local  |	4GB Ram, 2vcpus |
| Worker-01  |	worker01.techinet.local  |	4GB Ram, 2vcpus |

There are two server types used in deployment of Kubernetes clusters:
- Master: A Kubernetes Master is where control API calls for the pods, replications controllers, services, nodes and other components of a Kubernetes cluster are executed.
- Node: A Node is a system that provides the run-time environments for the containers. A set of container pods can span multiple nodes.

The minimums:
- Memory: 4 GiB or more of RAM per machine.
- CPUs: At least 2 CPUs on the control plane machine.
- Internet connectivity and internal connectivity between nodes.

