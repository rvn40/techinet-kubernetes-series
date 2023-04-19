# Setup Kubernetes Cluster with minikube on Ubuntu

## Prerequisite


| Hostname |	Specs |
| --- | --- |
| minikube-01  |	16GB Ram, 4vcpus |

## Instructions

For instruction in video format:

[![Setup Kubernetes Cluster with minikube on Ubuntu](https://i.ytimg.com/vi/jNFAvZOZSGc/hqdefault.jpg)](https://www.youtube.com/embed/jNFAvZOZSGc)

#### Update your system
Once the servers are ready, update them first.
```
sudo apt -y full-upgrade && sudo reboot
```

##### Install dependencies
```
sudo apt install curl vim -y
```
##### Add docker repository
```
sudo apt update -y && sudo apt install -y curl gnupg2 software-properties-common apt-transport-https ca-certificates
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

##### Install docker
```
sudo apt update -y && sudo apt install -y containerd.io docker-ce docker-ce-cli
```

```
sudo systemctl daemon-reload && sudo systemctl restart docker && sudo systemctl enable docker
```

#### Download and install Minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

sudo install minikube /usr/local/bin/
```

#### Verify the installation
```
minikube version
```

#### Start Minikube
```
minikube start
```

#### Check the status of your Minikube cluster
```
minikube status
```

You should now have Minikube up and running on your Ubuntu machine. You can start deploying and testing Kubernetes applications locally using Minikube.


### Deploy nginx webserver on minikube
#### Create an Nginx deployment
```
kubectl create deployment nginx --image=nginx
```

#### Verify the deployment
```
kubectl get deploy
```

#### Create an Nginx service to expose the deployment
```
kubectl expose deployment nginx --port=80 --type=NodePort
```

#### Verify the service:
```
kubectl get services
```

#### Get the IP address of the Minikube node:
```
minikube ip
```

#### Get the IP address of the Minikube node:
```
kubectl describe service nginx
```

#### Access the Nginx webserver using the Minikube node's IP address and NodePort:
```
curl http://<minikube-ip>:<node-port>
```

You should now see the default Nginx web page displayed in the terminal. 


