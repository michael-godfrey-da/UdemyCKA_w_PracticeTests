# Created Automatically:
- Default
- kube-system (internal kubernetes, dns service, etc)
- kube-public (where resources for all users should be)

resources can use simple name as DNS hostname w/in a namespace

DNS entry:
<name>.<namespace>.svc.cluster.local
(ie. <name>.<namespace>.svc(subdomain).cluster.local(domain))

`k get namespace`
`k create namespace <namespace name>`

--namespace=<namespace>
e.g. `k get pods --namespace=dev`

## to set current context namespace
`kcnf set-context $(kcnf current-context) --namespace=<namespace>

## `--all-namespaces`
e.g. `k get pods --all-namespaces`

## Resource Quotas