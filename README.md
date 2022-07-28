# Terraform Google Cloud Deploy GKE Cluster
[Reference 1](https://learn.hashicorp.com/tutorials/terraform/gke)<br/>
[Reference 2](https://registry.terraform.io/providers/hashicorp/google/latest/docs/guides/using_gke_with_terraform)<br/>
[Reference 3](https://github.com/antonputra/tutorials/tree/main/lessons/069)<br>
Provision of kubernetes cluster in google cloud platform with terraform and runing Vote application and flask application<br>
To configure gcloud sdk on Mac
``` 
brew install --cask google-cloud-sdk
```
```
gcloud init
```
```
gcloud auth application-default login
```
# Setup and Initialize Terraform 
Update terraform.tfvars file with your project_id, and region<br/>
You can easily get your prooject_id by running<br>
```
gcloud config get-value project
```
Start Provision with Terraform 
```
terraform init -upgrade
```
```
terraform apply
```
Configure kubectl
```
gcloud container clusters get-credentials $(terraform output -raw kubernetes_cluster_name) --region $(terraform output -raw region)
```
```
kubectl get all
```
Now you are connected to GKE cluster and you should see something similar<br>
Running Vote app and Flask app on kubernetes cluster<br/>
Copy azure-vote.yaml and flask-app.yaml files into learn-terraform-provision-gke-cluster folder<br/>

```
kubectl apply -f azure-vote.yaml            
```
```
kubectl apply -f flask-app.yaml            
```
```
Kubectl get all
```
Now you access both applications via External-IP addresses <br/>
You should see on browser something like <br>

# Clean up Resources 
```
terraform destroy
```





