## Node Selectors and 

`nodeSelector` in conf under spec

### e.g. Node Selectors

#### Labelling the node
`k label nodes node1 size=Large`

#### Pod Config
```yaml
spec:
  containers:
  - name:data-processod
    image: dataprocesor
  nodeSelector:
    size: Large
```

### Node Affinity

#### Node Affinity Types:
- requiredDuringSchedulingIgnoredDuringExecution
- preferredDuringSchedulingIgnoredDuringExecution
- requiredDuringSchedulingRequiredDuringExecution (planned)

eg.
pod-definition.yaml
```yaml
spec:
  containers:
  - name:data-processor
    image: data-processor
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: size
            operator: In # NotIn, Exists, DoesNotExist
            values:
            - Large
```