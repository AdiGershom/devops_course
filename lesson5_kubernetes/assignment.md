## Part 0 – Prerequisites
gersha2@GERSHA2-HR6W57R659 devops_course % `kubectl get nodes `  
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   5d    v1.35.0

gersha2@GERSHA2-HR6W57R659 lesson5_kubernetes % `kubectl get namespaces`

NAME              STATUS   AGE
default           Active   5d
dev               Active   4d2h
kube-node-lease   Active   5d
kube-public       Active   5d
kube-system       Active   5d


## Part 1 – Namespace (Logical Separation)
Namespace is a logic folder in the cluster
it's logic and not a pyscal because there is no pyscal server, all the namespaces run on the same nodes and the same infrustructers.

ersha2@GERSHA2-HR6W57R659 lesson5_kubernetes % `kubectl get namespaces`

NAME              STATUS   AGE
default           Active   5d
dev               Active   4d2h
kube-node-lease   Active   5d
kube-public       Active   5d
kube-system       Active   5d
## Part 2 – Pod (Ephemeral Workload)

gersha2@GERSHA2-QX2VWJYYQJ lesson5_kubernetes % `kubectl get pods -n dev`

NAME       READY   STATUS    RESTARTS   AGE
demo-pod   1/1     Running   0          11h

Question:
 What happens if you delete this Pod? Who recreates it?
Nothing happens. The Pod is not recreated because it was created manually and is not managed by a Deployment (or any controller)

JYYQJ lesson5_kubernetes % `kubectl get rs -n dev`

NAME                       DESIRED   CURRENT   READY   AGE
app-deployment-c8c47c4dd   3         3         3       5m45s
gersha2@GERSHA2-QX2VWJYYQJ lesson5_kubernetes % `kubectl get deployments -n dev`

NAME             READY   UP-TO-DATE   AVAILABLE   AGE
app-deployment   3/3     3            3           5m57s
gersha2@GERSHA2-QX2VWJYYQJ lesson5_kubernetes % `kubectl get pods -n dev`

NAME                             READY   STATUS    RESTARTS   AGE
app-deployment-c8c47c4dd-cvn4f   1/1     Running   0          6m30s
app-deployment-c8c47c4dd-lrd4n   1/1     Running   0          6m30s
app-deployment-c8c47c4dd-sdtsv   1/1     Running   0          6m30s
demo-pod                         1/1     Running   0          11h

##  Part 3 – Deployment (Desired State)

Which object ensures the number of Pods?
the Replicaset is response to make sure there are 3 pods up, if some pod removed- it will recreate it.
Why should Pods not be managed directly?
because the pods are temporery, they won't managed or recreate authomaticly

## Part 4 – Deployment → ReplicaSet → Pod Relationship

How many ReplicaSets exist after the update?
2 (the old one and the new)
Why does Kubernetes create a new ReplicaSet?
Because I updated the image to latest
it create new replicaset only if there is any change/update
if I just want to scale the deployment-there is no new replicaset

## Part 5 – Service Types
Which Service is internal only?
ClusterIP- aviable only internal the cluster

Which Service is best for production?
Load balancer- work with external ip from the cloud and provide clients aceess to the internet

## Part 6 – Ingress (HTTP Routing)
Does Ingress work without an Ingress Controller?
No. Ingress is just a resource that defines routing rules. It cannot route traffic by itself
it have to work with the ingress controller

Why not expose every Service directly?
Exposing every Service is hard to manage, insecure, and doesn’t support smart routing. Ingress gives a single entry point for easier control and load balancing.

## Part 7 – ConfigMap & Secret




