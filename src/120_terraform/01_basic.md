# Basic

### Links
* creating and applying IAM roles to terraform - https://medium.com/@gmusumeci/how-to-create-an-iam-account-and-configure-terraform-to-use-aws-static-credentials-a8ea4dd4fdfc
* creating vpc - https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc

### General
* infrastructure provisioning - store your cloud infrastructure set up as code
* like CloudFormation, but for many cloud providers i.e. AWS, Google, Azure, CloudFlare  

### Installation AWS
1. https://www.terraform.io/downloads.html
2. open from commander
3. aws provider -  https://registry.terraform.io/providers/hashicorp/aws/latest/docs
```terr
provider "aws" {
  region = "us-east-1"
}
```
4. terraform init

### Commends 
* *terraform init* - initial project
* *terraform apply* - apply script
* *terraform show* - inspect current state
* *terraform destroy* - destroy all resources created by configuration
