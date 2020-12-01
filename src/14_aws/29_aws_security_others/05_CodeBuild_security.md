### CodeBuild Security ###
* to access resources in your VPC, make sure you specify a VPC configuration ofr your CodeBuild
* secrets in CodeBuild
* don't store them as plaintext in environment variables
* instead...
    * environment variables can reference parameter store parameters
    * environment variables can reference secrets manager secrets

