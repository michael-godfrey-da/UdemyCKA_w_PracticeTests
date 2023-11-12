# DaemonSets

Ensures one copy of each pod is run in each node of the cluster (e.g. monitoring agents)

eg. kube-proxy

`k create -f daemonset-definition.yaml`

`k get daemonsets`

# To create a daemonset:
1. Create a deployment: `k create deployment ... -o yaml > daemonset.yaml`
2. Delete the `replicas`, `strategy` and `status` in the conf
3. Change `Deployment` to `DaemonSet` in the conf
4. `k apply -f daemonset.yaml`