## Taints and Tolerations

Taints are on nodes, tolerations are on pods

`k taint nodes node1 key=value:taint-effect`

### taint-effects: 
- NoScehdule
- PreferNoSchedule
- NoExecute

### Tolerations:
`tolerations` are part of pod effect

```yaml
tolerations:
- key: "value"
  operator: "Equal"
  value: "value"
  effect: "NoSchedule"
```

### Master Node
Master node has taints by default with `NoSchedule`

- describe master node to see taints