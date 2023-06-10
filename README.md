# devops-tools
============================================================================================================
# Git
## Install
```sh
sudo apt-get update
sudo apt-get install git
```
## Verify
```sh
git --version
```
============================================================================================================
# Docker
## Installation
```sh
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt update
sudo apt install docker-ce -y
sudo systemctl start docker
sudo systemctl enable docker
systemctl status docker
sudo usermod -aG docker ${USER}
newgrp docker
```
## Verify
```sh
docker --version
```
============================================================================================================
# Docker-Compose
## installation
```sh
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose –version
```
## Verify
```sh
docker-compose --version
```
============================================================================================================
# K3s
## Install Kubernetes Cluster(k3s)
Map the hostnames on each node
```sh
sudo vim /etc/hosts
172.16.10.3 master
172.16.10.4 worker01
172.16.10.10 worker02

install k3s
curl -sfL https://get.k3s.io | sh -s - --

check service status
systemctl status k3s

check nodes
sudo kubectl get nodes -o wide

You need to extract a token form the master that will be used to join the nodes to the master.
master
sudo cat /var/lib/rancher/k3s/server/node-token

Install k3s on worker nodes and connect them to the master
curl -sfL http://get.k3s.io | K3S_URL=https://<master_IP>:6443 K3S_TOKEN=<join_token> sh -s - --docker
sudo systemctl status k3s-agent
sudo kubectl get nodes
```
============================================================================================================
# Helm
## Install Helm Commandline tool on k3s
```sh
wget https://get.helm.sh/helm-v3.12.0-linux-amd64.tar.gz
tar -xvzf helm-v3.12.0-linux-amd64.tar.gz
sudo mv linux-amd64/helm /usr/local/bin/helm 
helm version
```
============================================================================================================
# Nginx-ingress
## Installation
```sh

```
============================================================================================================
# Rancher
## Installation
```sh
helm repo add rancher-stable https://releases.rancher.com/server-charts/stable
create namespace cattle-system
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.0/cert-manager.crds.yaml
helm repo add jetstack https://charts.jetstack.io
helm repo update
helm install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version v1.11.0
kubectl get pods --namespace cert-manager
helm install rancher rancher-stable/rancher --namespace cattle-system --set hostname=rancher.theeducloud.com --set bootstrapPassword=admin
```
## Verify
```sh
kubectl get ns
kubectl get pods -n cattle-system
kubectl get service -n cattle-system
kubectl get ingress -n cattle-system
```
============================================================================================================
