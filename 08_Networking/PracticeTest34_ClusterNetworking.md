# Cluster Networking

To get IPs
k get node -o wide

``` bash
ip link
ip a
ip link show type bridge

# To view networks/ports
netstat -nplt

# To view client connections to etcd
netstat -anp | grep etcd
```