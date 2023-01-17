# Setup Kubernetes Cluster with kubeAdm on Ubuntu

My setup contain two servers. One as control plane machine node and the other one as a worker node to be used for running containerized workloads. You can add more nodes to suit your desired use case, load, and HA.

| Role |	Hostname |	Specs |
| --- | --- | --- |
| Master  |	master01.techinet.local  |	4GB Ram, 2vcpus |
| Worker-01  |	worker01.techinet.local  |	4GB Ram, 2vcpus |

