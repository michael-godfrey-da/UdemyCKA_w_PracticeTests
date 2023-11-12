## Imperative - Explicit Commands

Create Examples:
- `k run nginx --image=nginx`
- `k create deployment --image=nginx nginx`
- `k expose deployment nginx --port 80`

Update Examples:
- `k edit deployment nginx`
- `k scale deployment nginx --replicas=5`
- `k set image deployment nginx nginx=nginx:1.9.1`

Also:
- `k create -f nginx.yaml`
- `k replace -f nginx.yaml`
- `k delete -f nginx.yaml`

## Declarative - YAML Files

`k apply -f nginx.yaml` (create or update based on current state)