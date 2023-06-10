# devops-tools
==================================================================================================================
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
==================================================================================================================
