# Cluster Upgrade

To check kubernetes version on each node:
`k get node`

To check OS version kubernetes is running on:
`cat /etc/*release*`

To check available updates:
```bash
apt update
apt-cache madison kubeadm
```

*Upgrade controlplane first!*

```bash
apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=1.25.10 && \
apt-mark hold kubeadm

```
To verify kubeadm version upgrade:
``` bash
kubeadm version
kubeadm upgrade plan

kubeadm upgrade apply v1.25.10
```

** This doesn't update kubelet ** 


to upgrade kubelet:

```bash
k drain controlplane --ignore-daemonsets

apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.25.10-00 kubectl=1.25.10-00 && \
apt-mark hold kubelet kubectl

# The restart kubelet

sudo systemctl daemon-reload
sudo systemctl restart kubelet

k uncordon controlplane
``

for other node:
1. ssh into node
2. upgrade kubeadm
3. drain node (from controlplane)
4. upgrade kubelet
```bash

ssh node01
apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=1.25.10 && \
apt-mark hold kubeadm

# from controlplane
sudo kubeadm upgrade node

# back on node
apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.25.10-00 kubectl=1.25.10-00 && \
apt-mark hold kubelet kubectl


# The restart kubelet
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```