# Multiple Schedulers

ServiceAccounts and ClusterRoleBindings were not explained... 
`kubectl get serviceaccount -n kube-system`
`kubectl get clusterrolebinding`

To view custom scheduler:
`k get events`

ConfigMap as a volume: ???

An exmaple using a custom scheduler
``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
  schedulerName: my-scheduler
```

## Scheduler Profiles

No fucking clue...

https://github.com/kubernetes/community/blob/master/contributors/devel/sig-scheduling/scheduling_code_hierarchy_overview.md

https://kubernetes.io/blog/2017/03/advanced-scheduling-in-kubernetes/

https://jvns.ca/blog/2017/07/27/how-does-the-kubernetes-scheduler-work/

https://stackoverflow.com/questions/28857993/how-does-kubernetes-scheduler-work