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