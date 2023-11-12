# Commands and Arguments

Docker Commands


```
FROM Ubuntu
ENTRYPOINT ["sleep"]
CMD ["5"] 
```


User args in yaml to send args to docker container 

```
apiVersion: v1
kind: Pod
metadata:
    name: ubuntu-sleeper-pod
spec:
    containers:
    - name: ubuntu-sleeper
      image: ubuntu-sleeper
      command: ["sleep", "10"]
```