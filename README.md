# Learn Terraform - Provision an EKS Cluster
## Initialize Terraform workspace
```
terraform init
```
## Provision EKS Cluster
```
terraform apply
```

Confirm the apply with `yes`

Your terminal prints the outputs defined in `outputs.tf`

## Configure kubectl
```
aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name) --profile $profile
```

## Deploy and access Kubernetes Dashboard
### Deploy Kubernetes Metrics Server
Download and unzip the metrics server by running the following command.
```
wget -O v0.3.6.tar.gz https://codeload.github.com/kubernetes-sigs/metrics-server/tar.gz/v0.3.6 && tar -xzf v0.3.6.tar.gz
```

Deploy the metrics server to the cluster by running the following command.
```
kubectl apply -f metrics-server-0.3.6/deploy/1.8+/
```

Verify that the metrics server has been deployed. If successful, you should see something like this.
```
kubectl get deployment metrics-server -n kube-system
```

### Deploy Kubernetes Dashboard

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta8/aio/deploy/recommended.yaml
```

```
kubectl proxy
```




