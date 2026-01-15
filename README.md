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
### Initialise the VM


## Sources
* 
