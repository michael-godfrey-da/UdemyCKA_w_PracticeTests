# DNS

## DNS in Kubernetes

eg.
```bash
curl http://kubernetes.default.svc.cluster.local


# for service:
# - host name (resource name): `web-service`
# - namespace: `apps`
# - type: `service` or `svc`
# - cluster root domain: `cluster.local`
curl http://web-service.apps.svc.cluster.local

#  for pod:
# - host name (ip w/dashes for dots): `10-244-2-5`
# - namespace: `apps`
# - type: `pod`
# - cluster root domain: `cluster.local`
curl http://10-244-2-5.apps.pod.cluster.local
```

## CoreDNS

### remember... `/etc/hosts` for hardcoded and `/etc/resolv.conf` for nameserver

### CoreDNS /etc/coredns/Corefile

```Corefile

kubernetes cluster.local ... {
    pods insecure
    upstream
    fallthrough in-addr.arpa ip6.arpa
}
```

Corefile is passed to pod as Configmap

To view:
```bash
k get configmap coredns -n kube-system -o yaml
```

By default uses `kube-dns` as service in kube-system namespace