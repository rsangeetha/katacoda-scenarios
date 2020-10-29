<br>

## Check Kubernetes Clusters are Read

`kubectl get nodes`{{execute}}

## Installing Helm
	
 `curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash`{{execute}}
	
## NAM Helm Chart Download
	
`curl https://cdn.microfocus.com/free/43HQQphN3jU~/AM_50_HelmChart-1.0.0_EA.tgz?DZ5NrJj4EY9E8y64D9Y7bmgux_0F9Y8D2vc6qasm2mwjfDOQB1lIHhID6QR7CVS1YNdGdIKLnfH_ZSbYn1ii_RfJZYxJcuQLAsC1iWmOoR-MgXzlrGhZXmbQO-13qvGAXOTK761TucezCiy3Sg --output am.tgz`{{execute}}
	
Unzip am.tgz

`tar -xvf am.tgz`{{execute}}
		 

## Installing the NginX Ingress Controller

`helm repo add stable "https://charts.helm.sh/stable"`{{execute}}

`helm repo update`{{execute}}

`helm install nginx-ingress stable/nginx-ingress --set controller.publishService.enabled=true`{{execute}}

## Check Ingress is deployment status

`helm list`{{execute}}
`kubectl get all`{{execute}}

## Create Kubernetes namespace called 'nam' to deploy Access Manager components
	
`kubectl create namespace nam`{{execute}}


## Update Access Manager Helm Chart Values

`vi access-manager/values.yaml`{{execute}}

Search for ingress and change the enabled value to true

and also replace below values with right dns
	:%s/www.cloudac.com/2886795280-simba08.environments.katacoda.com
	:%s/www.cloudidp.com/2886795280-simba08.environments.katacoda.com
	:%s/www.cloudag.com/2886795338-simba08.environments.katacoda.com


## Get node01 IP address

`kubectl get nodes -o wide`{{execute}}


## Deploy Access Manager using below command and replace the IP address with node01 Internal IP

helm install --namespace nam access-manager access-manager --set global.amconfig.adminConsoleIP=172.17.0.16 --set global.amsecret.adminName=admin --set global.amsecret.adminPassword=novell --set am-ac.node=node01 --set ingress.enabled=true


Wait for few minutes(Approx 5 to 10 minutes) and watch for the status of NAM deployment

`kubectl get statefulset,pods --namespace nam`{{execute}}

The status of the pods should be ready and running as stated below


controlplane $ kubectl get statefulset,pods --namespace nam
NAME                                     READY   AGE
statefulset.apps/access-manager-am-ac    1/1     37m
statefulset.apps/access-manager-am-ag    1/1     37m
statefulset.apps/access-manager-am-idp   1/1     37m

NAME                          READY   STATUS    RESTARTS   AGE
pod/access-manager-am-ac-0    2/2     Running   0          37m
pod/access-manager-am-ag-0    1/1     Running   0          37m
pod/access-manager-am-idp-0   1/1     Running   0          37m



## 	To Access Admin console :
	Click (+) on the top of the terminal windows and select 'select port to view on Host2'
	
	
	Enter 2443 port and click display port -> will open /nps

	Login to admin console  using admin/novell credentials
	
	Create an IDP cluster ->  DNS should be of similar like 2886795280-8443-simba08.environments.katacoda.com and port of 443
	
	for user store use edir of ac, use node01 internal ip 172.17.0.16
	
	Once IDP cluster is created, the IDP cluster status will turn into Greent and Current.
	
	Goto Katacoda scenario terminal,
	
	Click (+) on the top of the terminal windows and select 'select port to view on Host2'
	
	
	Enter 8443 port and click display port -> will open /nidp/portal
	
	Enter admin/novell credentials
