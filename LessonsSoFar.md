1. Kubernetes is a massive departure from docker-compose (but maybe it shouldn't be)

Docker Compose roughly corresponds to a deployment. Or perhaps a statefulset, I wouldn't know since they aren't covered in CKA.

2. Every cluster is different - Every cluster is the same

Every cluster should support the same tools like kubectl and and etcdctl. Various workflows should be identical no matter what (how to export and restore the controlplane config, how to figure out what's running)

Minikube is so different from k8s is so different from k3s is so different from every cloud provider out there. Even worse, tools that seek to unify these things are overwhelmingly difficult to comprehend if you don't understand the basics.

3. There are best practices, but there's always aso more 