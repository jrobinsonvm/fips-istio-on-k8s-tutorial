# Istio on EKS Tutorial 


## For this tutorial we will be leveraging AWS's EKS and its addon option for Tetrate's FIPS 140-2 compliant and validate build of istio.   
### Tetrate has recently become the first company to reach the highest level, FIPS 140-2 verification for Istio.

##### [Tetrate has recently become the first company to reach the highest level, FIPS 140-2 verification for Istio](https://tetrate.io/blog/tetrate-istio-distro-achieves-fips-certification/
)



### Step 1. Install GetMesh
Getmesh performs the management and maintenance of your Istio deployments.  
https://docs.tetrate.io/getmesh-cli/install/install-and-update

1. Install GetMesh CLI 

<br/>

```
curl -sL https://istio.tetratelabs.io/getmesh/install.sh | bash
```
