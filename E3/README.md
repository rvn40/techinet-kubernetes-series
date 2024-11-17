# How to Build KubeADM K8s Cluster with Ansible on Ubuntu

## Prerequisite


| Hostname |	Specs |
| --- | --- |
| ansible-01  |	4GB Ram, 1vcpus |
| controlplane  |	4GB Ram, 4vcpus |
| worker  |	4GB Ram, 1vcpus |

## Instructions

For instruction in video format:

[<img src="https://storage.googleapis.com/techinet-public/youtube/thumbnails/KubeSeries/E3/thumbnail.png" width="560" height="315">](https://youtu.be/c3_e30f86PA)

#### Pre Installation steps
Configure the firewall rules that allow every kubernetes nodes to communicate to each other. Otherwise, you could follow like the image below to let the firewall rules open to any ports if the purpose for development only.

![Firewall Rules Example](https://storage.googleapis.com/techinet-public/youtube/thumbnails/KubeSeries/E3/gcp_firewall_rules.png "Firewall Rules Example").

Create new service account with particular privileges. Otherwise, you could make it like "super admin" access if the purpose for development only.