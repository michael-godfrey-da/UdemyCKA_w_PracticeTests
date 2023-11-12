# Monitoring Cluster Components

Node Level and Pod Level

## Metrics Server
- In-memory only
- Retrieves from pods

## Monitoring w/ Kubelet
- cAdvisor (Container Advisor)

Basic monitoring of containers
`minikube addons enable metrics-server`


``` sh
git clone https://github.com/kubernetes-incubator/metrics-server.git

# git clone https://github.com/kodekloudhub/kubernetes-metrics-server.git

k create -f deploy/1.8+/
``

`k top node`
`k top pod`