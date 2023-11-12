How many replicationcontrollers/replicasets in current namespace?
--
`k get replicationcontroller`
`k get replicaset`


replicationcontroller vs replicaset

ReplicaSet requires `selector` definition

`selector` identifies what pods fall under it

eg.
```yaml
selector:
    matchLabels:
        tier: frontend
```

How to update a ReplicaSet (e.g. just updated # of replicas)
--
`k replace -f replicaset-definition.yaml`
`k edit replicaset <replicaset name>`

How to directly scale a ReplicaSet
--
by conf:
`k scale --replicas=6 -f replicaset-definition.yaml`

by name:
`k scale --replicas=6 replicaset <replicaset name>`