# Role Based Auth

## API Groups

Kubernetes API Server (on master node)

Default Port is :6443

e.g. 
`curl https://localhost:6443/version`

e.g. 
`curl http://127.0.0.1:8080/api/v1/pods`
`curl http://127.0.0.1:8080/healthz`
`curl http://127.0.0.1:8080/apis`

## Authenticate into Kube API Server

```
curl http://localhost:6443 -k \
    --key /root/admin.key \
    --cert /root/admin.crt \
    --cacert /root/ca.crt
```
(also can use `kubectl proxy --port=8080`)

## Authorization

### Node Authorization
    Access within cluster for Kubelet
    Uses Node Authorizer 
    e.g. `system:node:<node_name>` certificate 

### Attribute Based Authorization

User or set of users with set of permissions

Assigned with JSON policy definition file

eg.
```
{"kind": "Policy", "apiVersion": "abac.authorization.kubernetes.io/v1beta1", "spec": {"user": "jane", "namespace": "*", "resource": "*", "apiGroup": "*", "nonResourcePath": "*"}}
```

Must be manually edited and requires restart of API server

### Role Based Authorization

Define roles and assign to users

(better b/c more standardized)

### Webhook Mode

Send user + action request to external service
e.g. `Open Policy Agent (OPA) `

### `AlwaysAllow` and `AlwaysDeny` are built in
`AlwaysAllow` is default

## Authorization Mode
set in `/etc/kubernetes/manifests/kube-apiserver.yaml`

Auth chain w/ Comma separated list

Default is:
`--authorization-mode=AlwaysAllow`

## Role Based Access Control (RBAC)
roles and role bindings

To list:
- `k get roles`
- `k get rolebindings`

To Test:
- `k auth can-i create pods --as jane --namespace default`
- `k auth can-i delete pods --as bob --namespace default`


### Role Definition yaml

e.g. `role-definition.yaml`

``` yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["create", "list", "delete"]
```

### Role Binding Definition yaml

e,g, `role-binding-definition.yaml`

``` yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: dev-user-binding
subjects:
- kind: User
  name: dev-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
    kind: Role
    name: developer
    apiGroup: rbac.authorization.k8s.io
```