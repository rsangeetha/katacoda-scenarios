
<br>
<br>
## Pod
Pods are the smallest, most basic deployable objects in Kubernetes. A Pod represents a single instance of a running process in your cluster. Pods contain one or more containers, such as Docker containers.



## Listing all running Pod

To list all running pod using kubectl command

`kubectl get pods`{{execute}}

The above command will return 'No resources found.'.  This is because currently no pods are running/deployed.