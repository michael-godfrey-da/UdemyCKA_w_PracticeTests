# Certificates API

```
#User Creates Key 
openssl genrsa -out jane.key 2048

# User generates certificate sign request object
openssl req -new -key jane.key -subj "/CN=jane" -out jane.csr

# Administrator receives and creates csr object

# encoding csr into base64
cat jane.csr | base64 | tr -d '\n'

# (see jane-csr.yaml below)

# Administrator approves csr
k get csr <name>
k certificate approve jane

k get csr jane -o yaml

```

jane-csr.yaml
``` yaml
apiVersion: certificates.k8s.io/v1beta1
kind: CertificateSigningRequest
metadata:
  name: jane
spec:
    groups:
    - system:authenticated
    usages:
    - digital signature
    - key encipherment
    - client auth
    request: <base64 encoded CSR>
    ```
    
    ```