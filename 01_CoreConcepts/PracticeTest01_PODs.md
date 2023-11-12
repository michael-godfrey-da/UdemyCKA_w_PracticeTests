How many pods in current namespace?
--
`k get pods`

How to create a pod w/ nginx image?
--
`k run nginx --image=nginx`

What image is a pod based on?
How many containers are in a pod?
What is the state of a pod/container?
--

`k describe pod nginx`
        
(more detailed summary info):
        
`k get pods -o wide`

To delete a pod
--
`k delete pod nginx`

To simulate creating a pod without actually doing it use `--dry-run=client` (`-o yaml` for yaml format)
--
`k run redis --image=redis123 --restart=Never --dry-run=client -o yaml > redis.yaml`

To create with a yaml file
--
`k create -f redis.yaml`