## _Resources_

```
kubectl api-resources
```

----

## _Quick Commands_

```
kubectl get all -n dev
```

```
kubectl delete all --all
```

```
watch -n 1 'kubectl get all -n dev'
```

```
watch -n 1 'kubectl get pods -n dev'
```

```
watch -n 1 'kubectl get svc -n dev'
```

```
kubectl logs $(kubectl get pods -n dev| grep -i 'kafka' | awk '{print $1}') -n dev -f
```

```
kubectl delete pod $(kubectl get pods -n dev| grep -i 'kafka' | awk '{print $1}') -n dev -f
```

----

## _Cluster_

```
kubectl cluster-info
```

```
kubectl get componentstatuses
```

----

## _Nodes_

```
kubectl get nodes
```

```
kubectl get nodes -o wide 
```

```
kubectl describe node <NODE_NAME>
```

### _Managing Nodes_

Drain

```
kubectl drain <NODE_NAME> --ignore-daemonsets
```

* Add --delete-emptydir-data to delete pods using emptyDir

unschedulable

```
kubectl cordon <NODE_NAME>
```

schedulable (undo cordon)

```
kubectl uncordon <NODE_NAME>
```

### _Labeling_

Add a label

```
kubectl label nodes <NODE_NAME> <LABEL_KEY>=<LABEL_VALUE>
```

Remove a label from a node

```
kubectl label nodes <NODE_NAME> <LABEL_KEY>-
```

### _Annotation_

```
kubectl annotate nodes <NODE_NAME> <ANNOTATION_KEY>=<ANNOTATION_VALUE>
```

----

## _Namespace_

```
kubectl create namespace <NAMESPACE_NAME>
```

```
kubectl get namespaces
```

```
kubectl describe namespace <NAMESPACE_NAME>
```

```
kubectl delete namespace <NAMESPACE_NAME>
```

----

## _Deployments_

```
kubectl create deployment <DEPLOYMENT_NAME> --image=<IMAGE_NAME>
```

```
kubectl get deployments
```

```
kubectl describe deployment <DEPLOYMENT_NAME>
```

```
kubectl delete deployment <DEPLOYMENT_NAME>
```

### _Deployment Advanced_

```
kubectl scale deployment <DEPLOYMENT_NAME> --replicas=3
```

```
kubectl set image deployment/<DEPLOYMENT_NAME> mycontainer=<new_IMAGE_NAME>
```

```
kubectl expose deployment <DEPLOYMENT_NAME> --type=LoadBalancer --name=<SERVICE_NAME>
```

### _Deployment Rollouts_

To record an resource change in deployment file use **`--record`**

```
kubectl <COMMAND_TO_CHANGE_ANY_RESOURCE> --record
```

```
kubectl rollout history deployment/<DEPLOYMENT_NAME>
```

```
kubectl rollout undo deployment/<DEPLOYMENT_NAME>
```

```
kubectl rollout undo deployment/<DEPLOYMENT_NAME> --to-revision=<REVISION>
```

----

## _Pod_

```
kubectl get pods
```

```
kubectl get pods -o wide
```

```
kubectl get pods --show-labels
```

```
kubectl get pods -l <LABEL_1>,<LABEL_2>
```

```
kubectl describe pod <POD_NAME>
```

```
kubectl delete pod <POD_NAME>
```

----

## _Service_

```
kubectl get services
```

```
kubectl describe service <SERVICE_NAME>
```

```
kubectl delete service <SERVICE_NAME>
```

----

## _Replicaset_

```
kubectl get rs
```

```
kubectl get rs <REPLICASET_NAME> -o yaml
```

```
kubectl get rs <REPLICASET_NAME> -o json
```

```
kubectl describe rs <REPLICASET_NAME>
```

```
kubectl delete rs <REPLICASET_NAME>
```

### _ReplicaSet advanced_

Scale

```
kubectl scale rs <REPLICASET_NAME> --replicas=5
```

Edit the ReplicaSet directly

```
kubectl edit rs <REPLICASET_NAME>
```

View events related to the ReplicaSet

```
kubectl get events --field-selector involvedObject.kind=ReplicaSet
```

List all pods created by the specific ReplicaSet

```
kubectl get pods --selector=<SELECTOR>
```

example

```
kubectl get pods --selector=app=my-app
```

----

## _ConfigMap_

```
kubectl create configmap <CONFIG_NAME> --from-literal=key1=value1 --from-literal=key2=value2
```

```
kubectl get configmaps
```

```
kubectl describe configmap <CONFIG_NAME>
```

```
kubectl delete configmap <CONFIG_NAME>
```

----

## _Secrets_

```
kubectl get secrets
```

```
kubectl create secret generic <SECRET_NAME> --from-literal=username=myuser --from-literal=password=mypass
```

```
kubectl describe secret <SECRET_NAME>
```

```
kubectl delete secret <SECRET_NAME>
```

----

## _Persistent Volume_

```
kubectl get pv
```

```
kubectl get pvc
```

```
kubectl describe pv <PV_NAME>
```

----

## _Logs_

```
kubectl logs <POD_NAME> -f
```

```
kubectl logs <POD_NAME> -c <CONTAINER_NAME>
```

----

## _Exec_

```
kubectl exec -it <POD_NAME> sh
```

## _Port Forward_

```
kubectl port-forward <POD_NAME> <FORWARD_PORT>:<ACTUAL_PORT>
```

----

## Minikube Commands

```
minikube start --nodes 2 -p local-cluster --driver=docker
```

```
minikube status -p local-cluster
```

```
minikube node add --worker -p local-cluster
```

```
minikube node delete <NODE_NAME> -p local-cluster
```

```
minikube dashboard --url -p local-cluster
```
----
