# Certificates

## Types
- Client
- Server
- Root/ CA

## File Convention
- `*.crt` or `*.pem` for public key/lock
- `*.key` or `*-key.pem` for private key

##  Kubernetes Services

### Server Components:
- kubeapi-server
    + apiserver.crt
    + apiserver.key
- etcd-server
    + etcdserver.crt
    + etcdserver.key
- kubelet server
    + kubelet.crt
    + kubelet.key

### Client Components:
- admin
    + admin.crt
    + admin.key
- kube-scheduler
    + scheduler.crt
    + scheduler.key
- kube-controller-manager
    + controller-manager.crt
    + controller-manager.key
- kube-proxy
    + kube-proxy.crt
    + kube-proxy.key

### Certificate Authority:
- ca.crt
- ca.key

## Create Certificates:

### CA (root) Certificate:

Generating Keys:
- `openssl genrsa -out <name>.key 2048`

Certificate Signing Request (CSRs - ca.csr):
- `openssl req -new -key ca.key -subj "/CN=KUBERNETES-CA" -out ca.csr`

Signing Certificates (ca.crt):
- `openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt`

### Admin Client Certificates:

Generating Keys:
- `openssl genrsa -out admin.key 2048`

Certificate Signing Request (CSRs - admin.csr):
- `openssl req -new -key admin.key -subj \"/CN=kube-admin/O=system:masters" -out admin.csr`

Signing Certificates (admin.crt):
- `openssl x509 -req -in admin.csr -CA ca.crt -CAkey ca.key -out admin.crt`

### Client Side Certificates:

Generating Keys:
- `openssl genrsa -out scheduler.key 2048`
- `openssl genrsa -out controller-manager.key 2048`
- `openssl genrsa -out kube-proxy.key 2048`

Certificate Signing Request (CSRs - client.csr):
- `openssl req -new -key scheduler.key -subj \"/CN=system:kube-scheduler" -out scheduler.csr`
- `openssl req -new -key controller-manager.key -subj \"/CN=system:kube-controller-manager" -out controller-manager.csr`
- `openssl req -new -key kube-proxy.key -subj \"/CN=system:kube-proxy" -out kube-proxy.csr`

Signing Certificates (scheduler.crt):
- `openssl x509 -req -in scheduler.csr -CA ca.crt -CAkey ca.key -out scheduler.crt`
- `openssl x509 -req -in controller-manager.csr -CA ca.crt -CAkey ca.key -out controller-manager.crt`
- `openssl x509 -req -in kube-proxy.csr -CA ca.crt -CAkey ca.key -out kube-proxy.crt`

### Server Side Certificates:

#### ETCD
- Can have multiple certs for each etcd peer
eg. 
    etcdserver.crt / etcdpeer1.key / etcdpeer2.key:

These are specified when starting etcd

#### Kube API Server
Requires alternate names specified in `openssl.cnf`
e.g. [alt_names]

passed in when creating CSR
e.g.
`openssl req -new -key apiserver.key -subj "/CN=kube-apiserver" -config openssl.cnf -out apiserver.csr`

### Kubelet Client Certificates

certs are named after node names

CN: system:node:<node_name>

## Admin Authentication
### Manual

eg. `curl https://kube-apiserver:6443/api/v1/pods --key admin.key --cert admin.crt --cacert ca.crt`

### Kubeconfig

kube-config.yaml:
``` yaml
apiVersion: v1
clusters:
- cluster:
    certificate-authority: ca.crt
    server: https://kube-apiserver:6443
  name: kubernetes
kind: Config
users:
- name: admin
  user:
    client-certificate: admin.crt
    client-key: admin.key
```
## Viewing Certificates

openssl x509 -in <cert>.crt -text -noout

Important Parts:
- Issuer (CA)
- Name in Subject: CN=<name>
- Alternate Names (Subject Alternative Name)
- Validity Period

journalctl -u kubelet

## container level debugging:
crictl ps -a
crictl logs <container id>