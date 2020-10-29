


Create a nginx pod using kubectl command.  This command will create a pod named 'nginx' using nginx docker image.

`kubectl run nginx --image=nginx`{{execute}}

The above command will return `deployment.apps/nginx created` means a pod is created successfully.

To see the pod is running or not, run the kubectl command

`kubectl get pods`{{execute}}

