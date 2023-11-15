# IP Address Management

CNI Says CNI Plugin must handle assigning IPs

eg. `IP-List.txt`

`host-local` plugin: assigns IPs from a range

(Also `DHCP`)

## IPAM: IP Address Management

Specifies how to assign IPs

eg. `/etc/cni/net.d/net-script.conf`

### Which networking solution is deployed?

e.g. `/etc/cni/net.d/10-weave.conflist`

Agents/Peers run as pods in `kube-system` namespace
(remember - run `ip link` to see interfaces created by CNI)

### What is the address range for an interface?

e.g. `ip addr show weave`

### What is the default gateway for a node?

``` bash
ssh <node_name>
ip route
```
