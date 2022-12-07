# Istio on EKS Tutorial 


## For this tutorial we will be leveraging AWS's EKS and its addon option for Tetrate's FIPS 140-2 compliant and validate build of istio.   
##### [Tetrate has recently become the first company to reach the highest level, FIPS 140-2 verification for Istio](https://tetrate.io/blog/tetrate-istio-distro-achieves-fips-certification/)

<br/>

## Section 1 - Cluster Setup and Installation 

### Step 1. Use the following command to create your EKS Cluster you wish to install istio.  

```
eksctl create cluster --nodes 1
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
