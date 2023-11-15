https://github.com/kodekloudhub/certified-kubernetes-administrator-course

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

## 1. Install a container runtime on all nodes

hint: for Containerd follow docker install steps, but use containerd.io instead of docker-ce

## 2. Configure cgroup drivers

copy-paste out (.toml) configuration for chosen container runtime (systemd?)

do on all nodes

## 3. Install kubeadm, kublet, kubectl

## 4. kubeadm init <args> (on master node)

kubeadm init --pod-network-cidr=10.244.0.0/16 --apiserver-advertise-address=<API Server IP>
(use `ip addr`)

## 5. Install weavenet on master node

May need to modify IPALLOC_RANGE in weavenet.yaml to match pod network cidr

eg.
` k edit ds weavenet -n kube-system`

## 6. 

wget https://github.com/containerd/containerd/releases/download/v1.7.8/containerd-1.7.8-linux-amd64.tar.gz
tar Cxvf /usr/local containerd-1.7.8-linux-amd64.tar.gz

wget https://github.com/opencontainers/runc/releases/download/v1.1.10/runc.amd64
install -m 755 runc.amd64 /usr/local/sbin/runc
wget https://github.com/containernetworking/plugins/releases/download/v1.3.0/cni-plugins-linux-amd64-v1.3.0.tgz
mkdir -p /opt/cni/bin
tar Cxzvf /opt/cni/bin cni-plugins-linux-amd64-v1.3.0.tgz


<!-- Now edit config.toml for systemd -->
vim /etc/containerd/config.toml
sudo systemctl restart containerd