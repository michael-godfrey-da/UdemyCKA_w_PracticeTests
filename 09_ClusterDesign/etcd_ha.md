# ETCD HA

## On having a Quorom
 Just have a minimum of 3 nodes

- `export ETCD_API = 3`
- `etcdctl put name john`
- `etcd get name`
- `etcd get / --prefix --keys-only`