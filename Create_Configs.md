# Cheatsheet for creating resources w/ Kubectl

`export dry="--dry-run=client -o yaml"`

## Deployment
``` bash
k create deployment my-nginx-deployment --image=nginx $dry
```

## Pod
``` bash
k run pod my-nginx-pod --image=nginx $dry
```
## Services

- `--port` port where service listens
- `--target-port` port where container/pod listens

### ClusterIP service


#### Generic:
``` bash
# --tcp=<port>:<target-port>
k create service clusterip my-nginx-service --tcp=80:8080 $dry
```

#### For a deployment called my-nginx-deployment:
``` bash
k expose deployment my-nginx-deployment --port=80 --target-port=80 $dry
```
### NodePort service

``` bash
k expose deployment my-nginx-deployment --port=80 --target-port=80 --type=NodePort  $dry
```

### LoadBalancer service

``` bash
k expose deployment my-nginx-deployment --port=80 --target-port=80 --type=LoadBalancer  $dry
```
note: requires livenessProbe and readinessProbe to be defined in yaml
``` yaml
livenessProbe:
  httpGet:
    path: /healthz
    port: 80
  initialDelaySeconds: 30
  periodSeconds: 10
readinessProbe:
  httpGet:
    path: /readiness
    port: 80
  initialDelaySeconds: 5
  periodSeconds: 10
```

## Role and RoleBinding
```
k create role my-role --resource=pod --verb=list --namespace=prod $dry

kubectl create rolebinding my-role-binding --role=my-role --user=my-user --namespace=prod $dry
```


## Configmaps

``` bash
# Literals:
kubectl create configmap my-config --from-literal=foo=bar --from-literal=baz=qux

# from (.env) file:
kubectl create configmap my-config --from-file=my-file.txt --from-env-file=my-env-file.env
```

## ServiceAccounts

``` bash
k create serviceaccount mike-sa $dry
```