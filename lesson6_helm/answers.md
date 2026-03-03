## Part 1 – Create Helm Chart

Deployment- Runs the application continusly and ensures the desired number on pods are always running. supports updates and rollbacks
(make sure the replicas number will be constant )

Service- Provides a stable network endpoint to access pod.
allow communication even when pods are recreated

DaemonSet- Ensure one pod runs on every node in the cluster
commonly used for monitoring or logging agent

job-running only one time and finish, if not succeed , will retry as BackoffLimit

CronJob- Runs jobs on a scheduled basis (like cron in linux)
used for recurring tasks.

ConfigMap- Stores non-sensative configuration data
Allows changing configuration without rebuilding images

Secret- Stores sensative data such as passwords or tokens, used securely by pods


## Part 2 – Deploy the Chart

gersha2@GERSHA2-HR6W57R659 myapp % `helm upgrade --install myapp .`
Release "myapp" does not exist. Installing it now.
NAME: myapp
LAST DEPLOYED: Wed Feb 11 17:24:05 2026
NAMESPACE: default
STATUS: deployed
REVISION: 1
DESCRIPTION: Install complete
TEST SUITE: None

** if there is a problem with pull image to minikube- we need to run this command:
`minikube image load busybox:1.36.1`

gersha2@GERSHA2-HR6W57R659 myapp % `kubectl get configmap`
NAME               DATA   AGE
kube-root-ca.crt   1      23m
myapp-config       1      17m

 myapp % `kubectl get secret`

NAME                          TYPE                 DATA   AGE
myapp-secret                  Opaque               1      21m
sh.helm.release.v1.myapp.v1   helm.sh/release.v1   1      21m
sh.helm.release.v1.myapp.v2   helm.sh/release.v1   1      10m
sh.helm.release.v1.myapp.v3   helm.sh/release.v1   1      10m

## Part 5 – ConfigMap and Secret Usage
ConfigMap = non-sensitive config

Secret = sensitive data

Can be used as environment variables or mounted files

Works in Deployments, DaemonSets, and other workload types



