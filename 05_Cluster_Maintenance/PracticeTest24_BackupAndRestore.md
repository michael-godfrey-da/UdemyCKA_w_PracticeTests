# Backup and Restore

## Get a config for everything:
k get all --all-namespaces -o yaml > all-deployments-services.yaml


## ETCD

## Manifests
`/etc/kubernetes/manifests/`

defaut endpoint: `--endpoints=[127.0.0.1:2379]`
### etcd.service
(typically at: `/etc/systemd/system`)

`--data-dir=/var/lib/etcd `

To backup etcd:
`etcdctl snapshot save snapshot.db`

 --endpoints=<LISTEN_CLIENT_URLS> --cacert=<CA_CERT> --cert=<SERVER_CERT> --key=<SERVER_KEY>

To get etcd backup info
`ETCDCTL_API=3 etcdctl snapshot status snapshot.db`

(idk what this is: ETCDCTL_API)
`ETCDCTL_API=3 etcdctl snapshot save snapshot.db`

To restore:
``` bash
service kube-apiserver stop
ETCDCTL_API=3 etcdctl snapshot restore snapshot.db --data-dir /var/lib/etcd-from-backup
systemctl daemon-reload
service etcd restart
service kube-apiserver start
```
```


k config get-clusters