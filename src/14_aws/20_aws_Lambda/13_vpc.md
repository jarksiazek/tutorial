### Lambda VPC ###
* By default
    * Lambda function is launched outside your own VPC (AWS-owned VPC)
    * cannot access to your VPC resources (RDS, ElasticCache, internal ELB, etc)

* Lambda in VPC
![](images/aim2.jpg)
    * define VPC id, the Subnet and Security Group
    * Lambda will create an ENI (Elastic Network Interface) in your subnet
    * Need Role: AWSLambdaVPCAccessExecutionRole  

* Lambda in VPC - Internet Access
![](images/aim3.jpg)
    * Lambda function in your VPC does not have internet access
    * deploying a Lambda function in a public subnet does not give it the Internet access or a public IP
    * to give the Internet access to Lambda function in a private subnet gives it internet access (NAT Gateway/ Instance)
    * you can use VPC endpoints to privately access AWS services without a NAT 
    * note: Lambda - CloudWatch works even without endpoint or NAT Gateway