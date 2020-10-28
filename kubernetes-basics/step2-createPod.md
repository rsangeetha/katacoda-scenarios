##Creating a Pod

Create a nginx pod using kubectl command.  This command will create a pod named 'nginx' using nginx docker image.

`kubectl run nginx --image=nginx` {{execute}}

After the about command success, check whether the pod is created or not using the kubectl command

`kubectl get pods` {{execute}}

