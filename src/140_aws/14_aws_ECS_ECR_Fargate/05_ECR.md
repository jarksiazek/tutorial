### ECR ###
* Elastic Container Registry
* private docker image repository
* access is controlled through IAM (permission errors => policy)  
* AWS CLI v1 login command (may be asked at the exam)
```bash 
$(aws ecr get-login --no-include-email region eu-west-1)    
```
* AWS CLI v2 login command
```bash 
aws ecr get-login-password region eu-west-1 | docker login --username AWS --password-stdin 12qweq.dkr.amazon.com    
```
* Docker push & pull:
    * docker push 1212.dfde.eu-west-1.amazonaws.com/demo:latest
    * docker pull 1212.dfde.eu-west-1.amazonaws.com/demo:latest