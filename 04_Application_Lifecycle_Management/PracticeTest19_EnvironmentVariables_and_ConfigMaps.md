# Environment Variables and ConfigMaps


## Plain Key-Value Approach
e.g.
`docker -e APP_COLOR=pink simple-webapp-color`

And in a pod spec:
```yaml
spec:
    containers:
    - name: simple-webapp-color
      image: simple-webapp-color
      env:
      - name: APP_COLOR
        value: pink
```

## ConfigMap Approach
1. Create the ConfigMap

literal:
`k create configmap <config-map-name> --from-literal=<key>=<value>`

from file:
`k create configmap <config-map-name> --from-file=file.properties`


2. Inject ConfigMap into pod spec

To inject a whole file:
``` yaml
envFrom:
    configMapRef:
        name: <config-map-name>
```

``` yaml
spec:
  containers:
  - env:
    - name: APP_COLOR
      valueFrom:
        configMapKeyRef:
          name: webapp-config-map
          key: APP_COLOR
```
