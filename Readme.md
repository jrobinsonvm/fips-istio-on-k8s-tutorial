# Istio on EKS Tutorial 


## For this tutorial we will be leveraging AWS's EKS and its addon option for Tetrate's FIPS 140-2 compliant and validate build of istio.   
##### [Tetrate has recently become the first company to reach the highest level, FIPS 140-2 verification for Istio](https://tetrate.io/blog/tetrate-istio-distro-achieves-fips-certification/)

<br/>

## Prerequisite -  Cluster Setup and Installation.  
#### - This example uses eksctl however feel free to deploy your cluster using your preferred method.   

### Use the following command to create an EKS Cluster you wish to install istio.  

```
eksctl create cluster --nodes 2
```
<br/>

-----------


## There are several supported ways to install tetrate's fips compliant istio distribution.  
#### - Section A - Uses the EKS Addon install method 
 - If you are not authorized to use AWS's Tetrate subscription, please follow Section B instead.  

#### - Section B - Uses a more generic install method which is suited for any kubernetes distribution including but not limited to EKS.   


<br/>

<br/>


## Section A - Istio Installation using EKS Addons (optional) 
 - If you are not authorized to use AWS's Tetrate subscription, please follow Section B instead.  

<br/>

### Step 1. Ensure Addon for Tetrate is available.  
- Subscription is required

```
aws eks describe-addon-versions --addon-name tetrate-io_istio-distro 
```

### Step 2. Deploy Addon to your newly created EKS Cluster 

```
aws eks create-addon --addon-name tetrate-io_istio-distro --cluster-name <CLUSTER_NAME>
```
The installation will take about 2 minutes to complete.   


### Step 3. Run the following command to verify that all components have been installed successfully.  

```
aws eks describe-addon --addon-name tetrate-io_istio-distro --cluster-name  <CLUSTER_NAME>
```

<br/>



## Section B - Istio Installation using GetMesh CLI 

### Step 1. Install GetMesh CLI 

```
curl -sL https://istio.tetratelabs.io/getmesh/install.sh | bash
```

### Step 2. Run GetMesh Version Command to validate install

```
getmesh version
```

### Step 3. List all GetMesh Istio versions available for install 

```
getmesh list
```

```
user@computer ~ % getmesh list
ISTIO VERSION	  FLAVOR   	FLAVOR VERSION	   K8S VERSIONS     
   1.16.0    	  tetrate  	      0       	1.22,1.23,1.24,1.25	
   *1.16.0   	tetratefips	      0       	1.22,1.23,1.24,1.25	
   1.16.0    	   istio   	      0       	1.22,1.23,1.24,1.25	
   1.15.3    	  tetrate  	      0       	1.22,1.23,1.24,1.25	
   1.15.3    	tetratefips	      0       	1.22,1.23,1.24,1.25	
   1.15.3    	   istio   	      0       	1.22,1.23,1.24,1.25	
   1.15.1    	  tetrate  	      0       	1.22,1.23,1.24,1.25	
   1.15.1    	tetratefips	      0       	1.22,1.23,1.24,1.25	
   1.15.1    	   istio   	      0       	1.22,1.23,1.24,1.25	
   1.14.5    	  tetrate  	      0       	1.21,1.22,1.23,1.24	
   1.14.5    	tetratefips	      0       	1.21,1.22,1.23,1.24	
   1.14.5    	   istio   	      0       	1.21,1.22,1.23,1.24	
   1.14.4    	  tetrate  	      0       	1.21,1.22,1.23,1.24	
   1.14.4    	tetratefips	      0       	1.21,1.22,1.23,1.24	
   1.14.4    	   istio   	      0       	1.21,1.22,1.23,1.24	
   1.14.3    	  tetrate  	      0       	1.21,1.22,1.23,1.24	
   1.14.3    	tetratefips	      0       	1.21,1.22,1.23,1.24	
   1.14.3    	   istio   	      0       	1.21,1.22,1.23,1.24	
   1.14.1    	  tetrate  	      0       	1.21,1.22,1.23,1.24	
   1.14.1    	tetratefips	      0       	1.21,1.22,1.23,1.24	
   1.14.1    	   istio   	      0       	1.21,1.22,1.23,1.24	
   1.13.7    	  tetrate  	      0       	1.20,1.21,1.22,1.23	
   1.13.7    	tetratefips	      0       	1.20,1.21,1.22,1.23	
   1.13.7    	   istio   	      0       	1.20,1.21,1.22,1.23	
   1.13.3    	  tetrate  	      0       	1.20,1.21,1.22,1.23	
   1.13.3    	tetratefips	      0       	1.20,1.21,1.22,1.23	
   1.13.3    	   istio   	      0       	1.20,1.21,1.22,1.23	
   1.13.2    	  tetrate  	      0       	1.20,1.21,1.22,1.23	
   1.13.2    	tetratefips	      0       	1.20,1.21,1.22,1.23	
   1.13.2    	   istio   	      0       	1.20,1.21,1.22,1.23	
   1.12.8    	  tetrate  	      0       	1.19,1.20,1.21,1.22	
   1.12.8    	tetratefips	      0       	1.19,1.20,1.21,1.22	
   1.12.8    	   istio   	      0       	1.19,1.20,1.21,1.22	
   1.12.6    	  tetrate  	      0       	1.19,1.20,1.21,1.22	
   1.12.6    	tetratefips	      0       	1.19,1.20,1.21,1.22	
   1.12.6    	   istio   	      0       	1.19,1.20,1.21,1.22	
   1.12.4    	  tetrate  	      0       	1.19,1.20,1.21,1.22	
   1.12.4    	tetratefips	      0       	1.19,1.20,1.21,1.22	
   1.12.4    	   istio   	      0       	1.19,1.20,1.21,1.22	
   1.11.8    	  tetrate  	      0       	1.17,1.18,1.19,1.20	
   1.11.8    	tetratefips	      0       	1.17,1.18,1.19,1.20	
   1.11.8    	   istio   	      0       	1.17,1.18,1.19,1.20	
   1.11.6    	  tetrate  	      1       	1.17,1.18,1.19,1.20	
   1.11.3    	  tetrate  	      0       	1.17,1.18,1.19,1.20	
   1.11.6    	tetratefips	      1       	1.17,1.18,1.19,1.20	
   1.11.3    	tetratefips	      0       	1.17,1.18,1.19,1.20	
   1.11.3    	   istio   	      0       	1.17,1.18,1.19,1.20	
   1.10.3    	  tetrate  	      0       	1.17,1.18,1.19,1.20	
   1.10.3    	tetratefips	      0       	1.17,1.18,1.19,1.20	
   1.10.3    	   istio   	      0       	1.17,1.18,1.19,1.20	

```

All of the above versions are available for use upon selection.    



### Step 4. Run the following command to fetch the latest version of istio available through getmesh. 
-  We will use the tetratefips flavor.  
-  This build represents the FIPS verified version.


```
getmesh fetch --version 1.16.0 --flavor tetratefips --flavor-version 0
```


### Step 5. Switch to the istio version you just downloaded via the fetch command 

```
getmesh switch --version 1.16.0 --flavor tetratefips --flavor-version=0
```

### Step 6.  Run getmesh show command to show the version of istio that has been configured.   

```
getmesh show
```

### Step 7. Install istio installing the demo profile.  

```
getmesh istioctl install --set profile=demo
```

### Step 8. Apply a label to the namespace(s) you wish to auto inject istio sidecars.  
- We are using the default namespace in this example.  

```
kubectl label namespace default istio-injection=enabled
```

### Step 9. Now lets use getmesh to validate our installation.  

```
getmesh config-validate
```

You should recieve a message similar to the following.

```
Your Istio configurations are healthy. Configuration issues not found.
```

### All done you have completed the installation of a FIPS compliant and validated version of istio!


<br/>

-------------------

<br/>

## Section 1 - Deploy a sample microservices application 
-  Deployment will not leverage istio's ingress capabilities.  
-  Section 2 will build on this deployment for ingress.  

### Step 1. Git clone the following repo to your desired workstation.  

```
git clone https://github.com/jrobinsonvm/microservices-demo.git
```


### Step 2. Switch to the application's directory 

```
cd microservices-demo
```


### Step 3. Deploy the app using kubectl
#### This deployment will not use istio's gateway but rather depend on an external load balancer to allow for a comparison. 

```
kubectl apply -f ./release/kubernetes-manifests.yaml
```


### Step 4. Lets use the get pods command with the wait option to monitor the status of our deployment.  

```
kubectl get pods -w
```


```
user@computer microservices-demo % kubectl get pods -w
NAME                                     READY   STATUS            RESTARTS   AGE
adservice-69d5d6555-smw4b                1/2     Running           0          12s
cartservice-6b9f55f654-4s847             1/2     Running           0          14s
checkoutservice-956bb9589-fnlgc          2/2     Running           0          17s
currencyservice-59f9b8bd47-cl8d7         0/2     PodInitializing   0          12s
emailservice-854747bbcc-8tnxk            2/2     Running           0          18s
frontend-6c75d7fd67-fc7pq                1/2     Running           0          16s
loadgenerator-7799d6949b-tzfjj           2/2     Running           0          14s
paymentservice-bbfdb6467-hvqzh           2/2     Running           0          16s
productcatalogservice-5ffd855ff4-xx7d7   2/2     Running           0          15s
recommendationservice-56767bbdb9-mk4rn   2/2     Running           0          17s
redis-cart-6f65887b5d-kvr4j              2/2     Running           0          11s
shippingservice-7dc9548cf7-njk7r         2/2     Running           0          11s
frontend-6c75d7fd67-fc7pq                2/2     Running           0          20s
currencyservice-59f9b8bd47-cl8d7         0/2     Running           0          21s
currencyservice-59f9b8bd47-cl8d7         1/2     Running           0          22s
currencyservice-59f9b8bd47-cl8d7         2/2     Running           0          23s
cartservice-6b9f55f654-4s847             2/2     Running           0          30s
adservice-69d5d6555-smw4b                2/2     Running           0          46s

```

### Step 5. Now lets grab the IP or FQDN of our frontend-external service.  

```
kubectl get service frontend-external | awk '{print $4}'
```

### Step 6. Try accessing the IP or Domain in your preferred browser or by running the following command.   

```
curl <IP-Address-or-FQDN>
```

<br/>

--------

## Section 2 - Leverage Istio's Ingress Capabilities to handle application traffic.   

### Step 1. Run the following command to deploy istio constructs for your application.  

```
kubectl apply -f ./release/istio-manifests.yaml
```

#### This will deploy the following components: 
- An ingress gateway to serve inbound traffic
- A virtual service for routing to backend hosts 
- Service entries for outbound traffic external to cluster 


```
user@computer microservices-demo % kubectl apply -f ./release/istio-manifests.yaml

gateway.networking.istio.io/frontend-gateway created
virtualservice.networking.istio.io/frontend-ingress created
serviceentry.networking.istio.io/allow-egress-googleapis created
serviceentry.networking.istio.io/allow-egress-google-metadata created
virtualservice.networking.istio.io/frontend created

```

### Step 2. Lets now grab the IP or FQDN of our Istio Ingress Gateway.  

```
kubectl get service istio-ingressgateway -n istio-system | awk '{print $4}'
```



