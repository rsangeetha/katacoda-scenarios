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


`helm repo add stable https://charts.helm.sh/stable`{{execute}}

`helm repo update`{{execute}}

`helm install nginx-ingress stable/nginx-ingress --set controller.publishService.enabled=true`{{execute}}


## Check Ingress is deployment status


`helm list`{{execute}}

`kubectl get all`{{execute}}


## Create Kubernetes namespace called 'nam' to deploy Access Manager components
	
`kubectl create namespace nam`{{execute}}


<!-- NEED TO CHECK THE BELOW COMMANDS ARE MANDATORY OR NOT -->

<!-- ## Update Access Manager Helm Chart Values

`vi access-manager/values.yaml`{{execute}}


Search for ingress and change the enabled value to true 

`:%s/enabled: false/enabled: true`{{execute}}



and also replace below values with right DNS


`:%s/www.cloudac.com/[[HOST_SUBDOMAIN]]-[[KATACODA_HOST]].environments.katacoda.com`{{execute}}

`:%s/www.cloudidp.com/[[HOST_SUBDOMAIN]]-[[KATACODA_HOST]].environments.katacoda.com`{{execute}}

`:%s/www.cloudag.com/[[HOST_SUBDOMAIN]]-[[KATACODA_HOST]].environments.katacoda.com`{{execute}}

`:wq`{{execute}}
-->

	
## Deploy Access Manager using below command and replace the IP address with node01 Internal IP

`helm install --namespace nam access-manager access-manager --set global.amconfig.adminConsoleIP=[[HOST2_IP]] --set global.amsecret.adminName=admin --set global.amsecret.adminPassword=novell --set am-ac.node=node01 --set ingress.enabled=true`{{execute}}


Wait for few minutes(Approx 5 to 10 minutes) and watch for the status of NAM deployment

`kubectl get statefulset,pods --namespace nam`{{execute}}

<b> The status of the pods should be ready and running as stated below </b>


<table width="385">
<tbody>
<tr>
<td width="257">NAME</td>
<td width="64">READY</td>
<td width="64">AGE</td>
</tr>
<tr>
<td>statefulset.apps/access-manager-am-ac</td>
<td>1/1</td>
<td>37m</td>
</tr>
<tr>
<td>statefulset.apps/access-manager-am-ag</td>
<td>1/1</td>
<td>37m</td>
</tr>
<tr>
<td>statefulset.apps/access-manager-am-idp</td>
<td>1/1</td>
<td>37m</td>
</tr>
</tbody>
</table>

<br>

<table width="513">
<tbody>
<tr>
<td width="257">NAME</td>
<td width="64">READY</td>
<td width="64">STATUS</td>
<td width="64">RESTARTS</td>
<td width="64">AGE</td>
</tr>
<tr>
<td>pod/access-manager-am-ac-0</td>
<td>2/2</td>
<td>Running</td>
<td>0</td>
<td>37m</td>
</tr>
<tr>
<td>pod/access-manager-am-ag-0</td>
<td>1/1</td>
<td>Running</td>
<td>0</td>
<td>37m</td>
</tr>
<tr>
<td>pod/access-manager-am-idp-0</td>
<td>1/1</td>
<td>Running</td>
<td>0</td>
<td>37m</td>
</tr>
</tbody>
</table>


## 	Access Admin console and Create IDP Cluster  :

Login to admin console  using admin/novell credentials

<a href="https://[[HOST2_SUBDOMAIN]]-2443-[[KATACODA_HOST]].environments.katacoda.com/nps"> https://[[HOST2_SUBDOMAIN]]-2443-[[KATACODA_HOST]].environments.katacoda.com/nps </a> 


Create an IDP cluster ->  DNS should be of <b>`[[HOST2_SUBDOMAIN]]-8443-[[KATACODA_HOST]].environments.katacoda.com`{{copy}}<b> and <b> port of 443 </b>

For user store use edir of ac, use node01 internal ip: `[[HOST2_IP]]`{{copy}}

Once IDP cluster is created, the IDP cluster status will turn into Greent and Current.

##  Access IDP User Portal

<B>Access IDP Portal </B>

 <a href="https://[[HOST2_SUBDOMAIN]]-8443-[[KATACODA_HOST]].environments.katacoda.com/nidp/portal">https://[[HOST2_SUBDOMAIN]]-8443-[[KATACODA_HOST]].environments.katacoda.com/nidp/portal </a> 
Enter admin/novell credential to login
