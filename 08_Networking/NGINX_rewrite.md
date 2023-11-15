# Ingress Rewrite Rules

look under metadata annotations:
    nginx.ingress.kubernetes.io/rewrite-target

    `/pay` becomes `/`

``` yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: test-ingress
  namespace: critical-space
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /pay
        backend:
          serviceName: pay-service
          servicePort: 8282
```



``` yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /$2
  name: rewrite
  namespace: default
spec:
  rules:
  - host: rewrite.bar.com
    http:
      paths:
      - backend:
          serviceName: http-svc
          servicePort: 80
        path: /something(/|$)(.*)
```

Path: 
- `/something`: Matches the literal string /something.
- `(/|$)`: Matches either a forward slash / or the end of the string $.
- `(.*)`: Matches any number of characters.

Target:
$2 is the second capture group from the regex in the path rule. In this case, it is the string after /something/

