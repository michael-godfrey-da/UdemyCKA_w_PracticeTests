# Network Policy

Note - For internal DNS Resolution, you can use the following command to get the IP Address of the DNS Service in the kube-system namespace:

``` bash
k get svc -n kube-system
```
This can be enabled by allowing egress traffic from the pod to the DNS service IP address on port 53.

``` yaml
...
  - ports:
    - port: 53
      protocol: UDP
    - port: 53
      protocol: TCP
```


e.g.

``` yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: my-network-policy
spec:
  podSelector:
    matchLabels:
      app: my-app
  policyTypes:
    - Ingress
  ingress:
    - from:
        - podSelector:
            matchLabels:
              role: db
        - namespaceSelector:
            matchLabels:
              name: my-namespace
      ports:
        - protocol: TCP
          port: 3306
```


``` yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-policy
spec:
    podSelector:
        matchLabels:
            role: db
    policyTypes:
        - Ingress
        - Egress
    ingress:
        - from:
            - podSelector:
                matchLabels:
                    name: api-pod
            namespaceSelector:
                matchLabels:
                    name: prod
            - ipBlock:
                cidr: 192.168.5.10/32
            ports:
                - protocol: TCP
                  port: 3306
    egress:
        - to:
            - ipBlock:
                cidr: 192.168.5.10/32
            ports:
                - protocol: TCP
                  port: 80
```

e.g. (long-ass specific yaml from the practice quiz)
``` yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: internal-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      name: internal
  policyTypes:
  - Egress
  - Ingress
  ingress:
    - {}
  egress:
  - to:
    - podSelector:
        matchLabels:
          name: mysql
    ports:
    - protocol: TCP
      port: 3306

  - to:
    - podSelector:
        matchLabels:
          name: payroll
    ports:
    - protocol: TCP
      port: 8080

  - ports:
    - port: 53
      protocol: UDP
    - port: 53
      protocol: TCP
```
