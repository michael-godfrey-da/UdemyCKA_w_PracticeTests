# Multi Container Pods



exec into a pod called app:

`kubectl -n elastic-stack exec -it app -- cat /log/app.log

Also know that there are multicontainer patterns known as:
- sidecar
- adapter
- ambassador
