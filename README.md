# k8s-129metric-server
## On Master node - Configure Kubernetes metric server - kubeadm 1.29  vresion

## Step1: Download Metrics Server Manifest

```
curl -LO https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

## Step2:Modify Metrics Server Yaml File


vim components.yaml


### Find the "- args:"  section under the container section, add the following line:

- --kubelet-insecure-tls

and 

#####     - --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname  ### commetnt out this line and add below line

- --kubelet-preferred-address-types=InternalIP


## Step 3: Deploy Metrics Server

Now, we are all set to deploy metrics server, run following kubectl command,

```
kubectl apply -f components.yaml
```


## Step 4: Verify Metrics Server Deployment
After deploying the Metrics Server, verify it’s status by checking the pods status which is running in the kube-system namespace,

```
kubectl get pods -n kube-system
```
## Step 5: Test Metrics Server Installation
Finally, you can test the metrics server by running following kubectl command,

#### kubectl get po -n kube-system  ## make sure metric server running 1/1

```
kubectl top nodes
kubectl get pods
```


# (OR ) -- Update file avilable, just execute below command

```
https://raw.githubusercontent.com/kloudbytes/k8s-129metric-server/main/metricserver-k8s1.29.yaml
```

