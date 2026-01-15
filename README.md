# Getting Started with Kubevirt
This repository contains information on start playing around with KubeVirt on a local machine using lightweight kubernetes

**Why this tutorial?**
The first time I tried this, I quicklky realised that most of the many tutorials that exist are outdated and I needed workarounds to make things work.

## What you need and will use
* A computer - I used a laptop but you can use a VM if you have a platform that does nested virtualisation
* Some linux and k8s skills - if things go wrong, hopefully the instructions will be clear
* k3s - I used k3s, but I am sure with a bit of tinkering it should work on microk8s or minukube as well.
* For this one I used Ubuntu, but again any supported linux distro should work

## Instructions
### k3s
Install k3s (the super easy way)
```
curl -sfL https://get.k3s.io | sh -
```
Wait a bit and validate that it is working - mostly you will have to use sudo or be root
```
sudo su -
```
Another useful command (required for virtctl to actually work)
```
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
```

### Install virtctl CLI
The easy way - still as root or use sudo
Get the latest version
```
export VERSION=$(curl https://storage.googleapis.com/kubevirt-prow/release/kubevirt/kubevirt/stable.txt)
wget https://github.com/kubevirt/kubevirt/releases/download/${VERSION}/virtctl-${VERSION}-linux-amd64
```
Put it somewhere you can run it
```
mv virtctl-${VERSION}-linux-amd64 virtctl
install virtctl /usr/local/bin/
```
There are other ways as well: https://kubevirt.io/user-guide/user_workloads/virtctl_client_tool/ 

### KubeVirt setup
Deploy the KubeVirt Operator
```
export VERSION=$(curl -s https://storage.googleapis.com/kubevirt-prow/release/kubevirt/kubevirt/stable.txt)
echo $VERSION
kubectl create -f "https://github.com/kubevirt/kubevirt/releases/download/${VERSION}/kubevirt-operator.yaml"
```
* There are some special instructions if you are using nested virtualisation here: https://kubevirt.io/quickstart_kind/
Deploy the custom resource definitions (so we can use the Operator)
```
kubectl create -f "https://github.com/kubevirt/kubevirt/releases/download/${VERSION}/kubevirt-cr.yaml"
```
Verify deployment
```
kubectl get kubevirt.kubevirt.io/kubevirt -n kubevirt -o=jsonpath="{.status.phase}"
# and/or
kubectl get all -n kubevirt
```
#### Containerized Data Importer
Containerized Data Importer - this allows us to import cloud images rather than just run up simple VMs
Enable the CDI
```
export VERSION=$(basename $(curl -s -w %{redirect_url} https://github.com/kubevirt/containerized-data-importer/releases/latest))
kubectl create -f https://github.com/kubevirt/containerized-data-importer/releases/download/$VERSION/cdi-operator.yaml
kubectl create -f https://github.com/kubevirt/containerized-data-importer/releases/download/$VERSION/cdi-cr.yaml
```
Verify the components are running
```
kubectl get cdi cdi -n cdi
```

### Import the VM


### Initialise the VM


## Sources
* 
