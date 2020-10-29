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

	
## Create Kubernetes namespace called 'nam' to deploy Access Manager components
	
`kubectl create namespace nam`{{execute}}


