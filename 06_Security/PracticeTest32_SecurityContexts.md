# Security Contexts

- Can be set at the pod level or the container level
- Pod level: applies to all containers in the pod
- Pod level: can override container level

e.g.
    
``` yaml
apiVersion: v1
kind: Pod
metadata:
    name: web-pod
spec:
    containers:
        - name: ubuntu
            image: ubuntu
            # sleep for 1 hour
            command: ["sleep", "3600"]
            securityContext:
                runAsUser: 1000
                capabilities:
                    add: ["MAC_ADMIN"]
```