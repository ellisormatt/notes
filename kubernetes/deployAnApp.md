```
kubectl create deployment deployment-name --image="url to image"
```
- searched for a suitable node where an instance of the application can be run
- scheduled the application ot run on that node
- configured the clusxter to reschedule the instance on a new node when needed
```
kubectl get deployments
```
```
kubectl proxy
```
- creates a proxy that will forward communications into the cluster-wide network
- after running the command, we have a connection between our host and the kubernetes cluster
```
kubectl exec -ti $POD_NAME bash
```
- opens a bash session into a pod
```
kubectl config set-context --current --namespace=kube-system
```
- set namespace for all future commands


--------------------------

# expose a service to access externally

```
kubectl expose deployment name-of-deployment --type=serviceType
kubectl expose deployment hello-minikube --type=NodePort
```
