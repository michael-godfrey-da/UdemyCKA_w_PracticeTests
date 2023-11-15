# CNI

## Pod Networking

Every Pod Should:
- Have a unique IP address
- Be able to communicate w/in same node
- Not need a NAT

## Kubelet CNI

First: `ps aux | grep kubelet`

Then:
- `--cni-bin-dir`: Supported CNI plugins (otherwise look in `/opt/cni/bin`)
- `--cni-conf-dir`: Config files for CNI plugins (otherwise look in `/etc/cni/net.d`)
- `--network-plugin`: idk... should just be `cni`?

To find CNI Executable:

- Look for `type` field in `/etc/cni/net.d/<CNI Conf File>.conflist`

## Container Runtime Endpoint
(I don't know what this is yet, but here's how to find it):

`ps aux | grep kubelet | grep container-runtime-endpoint`