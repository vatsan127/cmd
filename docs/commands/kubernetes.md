# Kubernetes

## Resources

```sh
kubectl api-resources
```

---

## Cluster

```sh
kubectl cluster-info
```

```sh
kubectl get componentstatuses
```

---

## Nodes

### Inspect

```sh
kubectl get nodes
```

```sh
kubectl get nodes -o wide
```

```sh
kubectl describe node <NODE_NAME>
```

### Scheduling

Drain a node (add `--delete-emptydir-data` to also evict pods using `emptyDir`).

```sh
kubectl drain <NODE_NAME> --ignore-daemonsets
```

Mark a node unschedulable.

```sh
kubectl cordon <NODE_NAME>
```

Mark a node schedulable again (undo cordon).

```sh
kubectl uncordon <NODE_NAME>
```

### Labels & Annotations

Add a label.

```sh
kubectl label nodes <NODE_NAME> <LABEL_KEY>=<LABEL_VALUE>
```

Remove a label from a node.

```sh
kubectl label nodes <NODE_NAME> <LABEL_KEY>-
```

Add an annotation.

```sh
kubectl annotate nodes <NODE_NAME> <ANNOTATION_KEY>=<ANNOTATION_VALUE>
```

---

## Namespace

```sh
kubectl create namespace <NAMESPACE_NAME>
```

```sh
kubectl get namespaces
```

```sh
kubectl describe namespace <NAMESPACE_NAME>
```

```sh
kubectl delete namespace <NAMESPACE_NAME>
```

---

## Deployments

### Basics

```sh
kubectl create deployment <DEPLOYMENT_NAME> --image=<IMAGE_NAME>
```

```sh
kubectl get deployments
```

```sh
kubectl describe deployment <DEPLOYMENT_NAME>
```

```sh
kubectl delete deployment <DEPLOYMENT_NAME>
```

### Scale & Expose

```sh
kubectl scale deployment <DEPLOYMENT_NAME> --replicas=3
```

```sh
kubectl set image deployment/<DEPLOYMENT_NAME> mycontainer=<new_IMAGE_NAME>
```

```sh
kubectl expose deployment <DEPLOYMENT_NAME> --type=LoadBalancer --name=<SERVICE_NAME>
```

### Rollouts

To record a resource change in the deployment, append **`--record`**.

```sh
kubectl <COMMAND_TO_CHANGE_ANY_RESOURCE> --record
```

```sh
kubectl rollout history deployment/<DEPLOYMENT_NAME>
```

```sh
kubectl rollout undo deployment/<DEPLOYMENT_NAME>
```

```sh
kubectl rollout undo deployment/<DEPLOYMENT_NAME> --to-revision=<REVISION>
```

---

## ReplicaSet

### Basics

```sh
kubectl get rs
```

```sh
kubectl get rs <REPLICASET_NAME> -o yaml
```

```sh
kubectl get rs <REPLICASET_NAME> -o json
```

```sh
kubectl describe rs <REPLICASET_NAME>
```

```sh
kubectl delete rs <REPLICASET_NAME>
```

### Scale & Edit

Scale.

```sh
kubectl scale rs <REPLICASET_NAME> --replicas=5
```

Edit the ReplicaSet directly.

```sh
kubectl edit rs <REPLICASET_NAME>
```

### Events & Pods

View events related to the ReplicaSet.

```sh
kubectl get events --field-selector involvedObject.kind=ReplicaSet
```

List all pods created by a specific ReplicaSet.

```sh
kubectl get pods --selector=<SELECTOR>
```

Example.

```sh
kubectl get pods --selector=app=my-app
```

---

## Pod

```sh
kubectl get pods
```

```sh
kubectl get pods -o wide
```

```sh
kubectl get pods --show-labels
```

```sh
kubectl get pods -l <LABEL_1>,<LABEL_2>
```

```sh
kubectl describe pod <POD_NAME>
```

```sh
kubectl delete pod <POD_NAME>
```

---

## Service

```sh
kubectl get services
```

```sh
kubectl describe service <SERVICE_NAME>
```

```sh
kubectl delete service <SERVICE_NAME>
```

---

## ConfigMap

```sh
kubectl create configmap <CONFIG_NAME> --from-literal=key1=value1 --from-literal=key2=value2
```

```sh
kubectl get configmaps
```

```sh
kubectl describe configmap <CONFIG_NAME>
```

```sh
kubectl delete configmap <CONFIG_NAME>
```

---

## Secrets

```sh
kubectl get secrets
```

```sh
kubectl create secret generic <SECRET_NAME> --from-literal=username=myuser --from-literal=password=mypass
```

```sh
kubectl describe secret <SECRET_NAME>
```

```sh
kubectl delete secret <SECRET_NAME>
```

---

## Persistent Volume

```sh
kubectl get pv
```

```sh
kubectl get pvc
```

```sh
kubectl describe pv <PV_NAME>
```

---

## Debugging

### Logs

```sh
kubectl logs <POD_NAME> -f
```

```sh
kubectl logs <POD_NAME> -c <CONTAINER_NAME>
```

### Exec

```sh
kubectl exec -it <POD_NAME> -- sh
```

### Port Forward

```sh
kubectl port-forward <POD_NAME> <FORWARD_PORT>:<ACTUAL_PORT>
```

### Watch & Bulk (namespace `dev`)

```sh
kubectl get all -n dev
```

```sh
kubectl delete all --all
```

```sh
watch -n 1 'kubectl get all -n dev'
```

```sh
watch -n 1 'kubectl get pods -n dev'
```

```sh
watch -n 1 'kubectl get svc -n dev'
```

Tail logs of the pod whose name matches `kafka`.

```sh
kubectl logs $(kubectl get pods -n dev | grep -i 'kafka' | awk '{print $1}') -n dev -f
```

Force-delete the pod whose name matches `kafka`.

```sh
kubectl delete pod $(kubectl get pods -n dev | grep -i 'kafka' | awk '{print $1}') -n dev --grace-period=0 --force
```

---

## Minikube

```sh
minikube start --nodes 2 -p local-cluster --driver=docker
```

```sh
minikube status -p local-cluster
```

```sh
minikube node add --worker -p local-cluster
```

```sh
minikube node delete <NODE_NAME> -p local-cluster
```

```sh
minikube dashboard --url -p local-cluster
```
