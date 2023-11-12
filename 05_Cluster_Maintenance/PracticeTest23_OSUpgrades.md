# OS Upgrades

## "drain" nodes from a pod (remove nodes and cordon the node)

```bash
k drain node-1
k drain node-1 --ignore-daemonsets

k uncordon node-1
```

