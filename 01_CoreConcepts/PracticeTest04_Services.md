# Service Types
- NodePort
    + NodePort (external port on node, must be :30000 to :32767)
    + Port (on service)
    + target port (on pod)
- ClusterIP
- LoadBalancer

`kubectl create service nodeport webapp-service --tcp=8080:8080 --node-port=30080 --dry-run=client -o yaml > service-definition.yaml`

Or simply:
`k expose deployment <deployment name> --port <port> --name=<service name>`
`k expose pod <pod name> --port <port> --name=<service name>`