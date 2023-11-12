# Cluster Roles

e.g. Nodes, PersistentVolumes, clusterroles, clusterrolebindings, certificatesigningrequests,namespaces

e.g.

```
k api-resources --namespaced=false
```

## clusterroles

roles but for clusters

e.g.
- Cluster Admin
- Storage Admin

e.g. cluster-admin-role.yaml
``` yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: cluster-admin
rules:
- apiGroups: [""]
  resources: [""]
  verbs: ["*"]
```

e.g. cluster-admin-role-binding.yaml
``` yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: cluster-admin-binding
subjects:
- kind: User
  name: admin
  apiGroup: rbac.authorization.k8s.io
roleRef:
    kind: ClusterRole
    name: cluster-admin
    apiGroup: rbac.authorization.k8s.io
```
