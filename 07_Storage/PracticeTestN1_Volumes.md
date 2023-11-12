# Volumes

To mount a host directory,

``` yaml
spec:
    containers:
    - name: mycontainer
        image: redis
        volumeMounts:
        - name: data-volume
            mountPath: /data
    volumes:
    - name: data-volume
        hostPath:
            path: /data
            type: Directory
    - name: pv-volume
        persistentVolumeClaim:
            claimName: claim-log-1
```


# PersistentVolume

There is no easy way to create a template, so here you go:

``` yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-log
spec:
  persistentVolumeReclaimPolicy: Retain
  accessModes:
    - ReadWriteMany
  capacity:
    storage: 100Mi
  hostPath:
    path: /pv/log
```

# PersistentVolumeClaim

same shit, here ya go:

``` yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: claim-log-1
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 50Mi
```