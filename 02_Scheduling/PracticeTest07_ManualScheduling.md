## Manual Scheduling

### with pod definition
Manually specify `nodeName`

### with pod binding object

``` bash
curl --header "Content-Type:application/json" --request POST --data '{"apiVersion":"v1", "kind":"Binding", "metadata":{"name":"pod-1"}, "target":{"apiVersion":"v1", "kind":"Node", "name":"node-1"}}' http://$SERVER/api/v1/namespaces/default/pods/$PODNAME/binding/
```