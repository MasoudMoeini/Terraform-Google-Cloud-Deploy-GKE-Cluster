# Terraform Google Cloud Deploy GKE Cluster
[Reference 1](https://learn.hashicorp.com/tutorials/terraform/gke)<br/>
[Reference 2](https://registry.terraform.io/providers/hashicorp/google/latest/docs/guides/using_gke_with_terraform)<br/>
[Reference 3](https://github.com/antonputra/tutorials/tree/main/lessons/069)<br>
[Reference 4](https://docs.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-portal?tabs=azure-cli#code-try-0)<br/>
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
Some changes for future gcloud auth are [here](https://cloud.google.com/blog/products/containers-kubernetes/kubectl-auth-changes-in-gke) <br/>
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
Now you are connected to GKE cluster<br>
Running Vote app and Flask app on kubernetes cluster<br/>
```
kubectl apply -f azure-vote.yaml            
```
```
kubectl apply -f flask-app.yaml            
```
```
Kubectl get all
```
```
kubectl get svc
```
Now you access both applications via External-IP addresses <br/>
```
Vote Application  -> http://EXTERNAL-IP
Flask Application -> http://EXTERNAL-IP:60000
```
You should see on browser something like <br>
<img width="643" alt="Screenshot 2022-07-28 at 12 34 34" src="https://user-images.githubusercontent.com/43514418/181575243-a3fd6071-0534-4d17-944c-c7b564cf7bd5.png"><br/>
<img width="425" alt="Screenshot 2022-07-28 at 12 34 00" src="https://user-images.githubusercontent.com/43514418/181575331-d7d92940-cf01-493f-a345-070756113b4e.png">
# Clean up Resources 
```
terraform destroy
```





