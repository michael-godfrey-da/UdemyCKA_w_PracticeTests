# Rolling Updates and Rollbakcs

`k rollout status deployment <deployment name>`

## Deployment Strategies:
StrategyType: `Recreate` vs `RollingUpdate`
rollout uses `strategy type: RollingUpdate` by default

e.g. 
`k apply -f deployment-definition.yaml --record`
vs 
`k set image <name>`


`RollingUpdate` creates a new replicaSet for the updated pods

This allows for:
`k rollout undo deployment/my-app-deployment`

kubectl get deployment my-app-deployment --export -o yaml > deployment-definition.yaml