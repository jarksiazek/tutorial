### Q1
The is a key requirement from an architecture point of view that the entire system is decoupled to ensure less dependency.  
Which of the following is an ideal service to use to decouple different parts of a system? 
* CodePipeline
* **Simple Queue Service = SQS**
    * SQS offers a secure, durable and avaiable hosted queue that lets you integrate and decouple distributed software systems and components.
    * SQS offers common constructs such and dead-letter queues and cost allocation tag, it provides a generic web service API and it can be accessed by any programing language.
* Simple Notification Service = SNS
* CodeBuild

### Q2
Company creating a new development environment. They want to make use of their existing Chef recipes which they use for their on-premisse configuration for servers in AWS.  
Which of the following service would be ideal to use? 
* Beanstalk
* **OpsWorks** 
    * https://aws.amazon.com/opsworks/
    * OpsWorks is configuration management service that provides managed instances of Chef and Puppet.  
    * Chef and Puppet are automation platform that allow you to use code to automate the configurations of your servers.
    * OpsWorks lets you use Chef and Puppet to automate how servers are configured, deployed and managed across EC2 instances or on-premise enviroments.
* CloudFormation 
* SQS 

### Q3
You need to setup a RESTful API service in AWS that would be serviced via the following url https://aaa.com/customers.  
Which of the following combination of services can be used for development and hosting of the RESTful service? (select 2)  
* **AWS Lambda and AWS API Gateway**
    * Lambda can be used to ohst the code na dAPI gateway can be used to access API's which point to AWS Lambda 
* AWS Cloudfront and Elastic Load Balancer
* **EC2 and Elastic Load Balancer**
    * API Service on EC2 and then user AWS Application Load balancer 
* SQS and CloudFront 
 