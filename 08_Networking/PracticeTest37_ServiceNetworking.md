# Service Networking


- Services are accessible everywhere in cluster (e.g. ClusterIP)
- NodePort services are externally accessible

Kube API Service IP addresses are assigned from the `--service-cluster-ip-range` CIDR range

e.g.

`kube-api-server --service-cluster-ip-range <ip-range>` (default is 10.0.0.0/24) 

Can look up with:

`ps aux | grep kube-apiserver`

To view rules created by kube-proxy:

`iptables -L -t nat | grep db-service`

To view logs for service related stuff:

(e.g. what kind of proxy is being used?)

`cat /var/log/kube-proxy.log`

## To get ip address range for pods

1. find internal-ip for a node: `k get node -o wide`
2. find interface that contains range: `ip addr`