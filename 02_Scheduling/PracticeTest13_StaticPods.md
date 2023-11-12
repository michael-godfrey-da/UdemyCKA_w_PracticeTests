# Static Pods

kubelet monitors:
    `/etc/kubernetes/manifests`
    (defined with `--pod-manifest-path` in `kubelet.service`)
    (defined with `staticPodConfig` in `kubeconfig.yaml`)`

`docker ps` in lieu of `k get pods`

To find the config file for a static pod:
`ps aux | grep kubelet | grep config=`

in this case: `cat /var/lib/kubelet/config.yaml | grep staticPod`

to find static pod on node

ssh <nodename>
