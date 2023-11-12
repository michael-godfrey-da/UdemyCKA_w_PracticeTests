`k create -f deployment-definition.yaml`
`k get deployments`
`k get all`

`kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml`

`k set image deployment <deployment name> <container name>=<new image>`