# Istio on EKS Tutorial 


## For this tutorial we will be leveraging AWS's EKS and its addon option for Tetrate's FIPS 140-2 compliant and validate build of istio.   
##### [Tetrate has recently become the first company to reach the highest level, FIPS 140-2 verification for Istio](https://tetrate.io/blog/tetrate-istio-distro-achieves-fips-certification/)

<br/>

## Section A - Cluster Setup and Installation using EKS Addons (optional) 

### Step 1. Use the following command to create an EKS Cluster you wish to install istio.  

```
eksctl create cluster --nodes 2
```

### Step 2. Ensure Addon for Tetrate is available.  (Subscription is required) 

```
aws eks describe-addon-versions --addon-name tetrate-io_istio-distro 
```

### Step 3. Deploy Addon to your newly created EKS Cluster 

```
aws eks create-addon --addon-name tetrate-io_istio-distro --cluster-name <CLUSTER_NAME>
```
The installation will take about 2 minutes to complete.   


### Step 4. Run the following command to verify that all components have been installed successfully.  

```
aws eks describe-addon --addon-name tetrate-io_istio-distro --cluster-name  <CLUSTER_NAME>
```

<br/>



## Section B - Cluster Setup and Installation using GetMesh CLI 

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
### We will use the tetratefips flavor.  This build represents the FIPS verified version.


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

### Step 8. Apply a label to the namespace(s) you wish to auto inject istio sidecars.  We are using the default namespace in this example.  

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

### Step 1. Git clone the following repo to your desired workstation.  

```
git clone https://github.com/jrobinsonvm/microservices-demo.git
```


### Step 2. Switch to the application's directory 

```
cd microservices-demo
```


### Step 3. Deploy the app using kubectl 

```
kubectl apply -f ./release/kubernetes-manifests.yaml
```


### Step 4. Lets use the get pods command to view the status of the deployment

```
kubectl get pods 
```

### Step 5. 
