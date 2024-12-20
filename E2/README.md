# Setup Kubernetes Cluster with Minikube on Ubuntu

## Prerequisite


| Hostname |	Specs |
| --- | --- |
| minikube-01  |	16GB Ram, 4vcpus |

## Instructions

For instruction in video format:

[<img src="https://storage.googleapis.com/techinet-public/youtube/thumbnails/KubeSeries/E2/thumbnail.png" width="560" height="315">](https://www.youtube.com/embed/_qXfWa476Ik)

#### Update your system
Once the servers are ready, update them first.
```
sudo apt -y full-upgrade && sudo reboot
```

#### Install dependencies
```
sudo apt install curl vim -y
```
##### Add docker repository
```
sudo apt update -y && sudo apt install -y curl gnupg2 software-properties-common apt-transport-https ca-certificates
```

```
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

##### Enable Non-Root User Access
```
sudo usermod -aG docker $USER
```

```
sudo reboot
```

#### Download and install Minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
```
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

#### Downloads kubectl with curl on Linux
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

#### Validate the binary (optional)
```
curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
```
```
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```

#### Install kubectl
```
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

#### Test to ensure the version you installed is up-to-date:
```
kubectl version --client
```


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


