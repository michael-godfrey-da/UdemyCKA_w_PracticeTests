# Secrets

## Approaches to Create:
### Imperative:

```bash
k create secret generic <secret_name> --from-literal=<key>=<value>
```

```bash
k create secret generic <secret_name> --from-file=app.properties
```

### Declarative

```bash
k create -f
```

## Base64 Encoding:
### to encode:

```bash 
echo -n 'admin' | base64
```

### to decode:

```bash 
echo -n 'YWRtaW4=' | base64 --decode
```

## YAML Files:

pod-definition.yaml
```yaml
spec:
    containers:
    - name: simple-webapp-color
      image: simple-webapp-color
      ports:
      - containerPort: 8080
      envFrom:
        - secretRef:
            name: app-secret
```

secret-data.yaml
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
data:
  DB_Host: bG9jYWxob3N0
  DB_User: YWRtaW4=
  DB_Password: cGFzc3dvcmQ=
```
