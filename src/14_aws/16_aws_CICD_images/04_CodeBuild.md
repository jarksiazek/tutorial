### AWS CodeBuild ###
* fully managed build service
* alternative to other build tools such as Jenkins
* continuous scaling (no servers to manage or provision - no build queue)
* pay for usage: time it takes to complete the builds
* leverages Docker under the hood for reproducible builds
* possibility to extend capabilities leveraging our own base Docker images
* secure: integration with KMS for encryption of build artifacts, IAM for build permissions and VPC for network security, CloudTrail for API calls logging
* build instruction can be defined in code (buildspec.yml file) 
* output logs to Amazon S3 & AWS CloudWatch Logs
* use CloudWatch Alarms to detect failed build and trigger notifications
* CloudWatch Events /AWS Lambda as Glue 
* SNS notifications
* Ability to reproduce CodeBuild locally to troubleshoot in case of errors
* Builds can be defined within CodePipeline or CodeBuild itself

## CodeBuild supports
* Java, Ruby, Python, Go, Node.js, Android, .NET Core, PHP
* Docker: extends any environment you like  

## CodeBuild how works
![](images/aim2.jpg)

## CodeBuild BuildSpec
* **buildspec.yml** file must be at the **root** of the code
* define environment variables:
    * plaintext variables
    * secure secrets: use SSM Parameter store
* phases:
    * install: install dependencies you may need for your build
    * pre build: final command to execute before build
    * **build: actual build commands**
    * post build: finishing touches (zip out for example)
* artifacts: what to upload to S3 (encrypted with KMS)
* cache: files to cache (usually dependencies) to S3 for future build speedup

## CodeBuild Local Build
* in case of need of deep troubleshooting beyond logs
* you can run CodeBuild locally on your desktop (after installing Docker)
* for this, leverage tje CodeBuild Agent

## CodeBuild in VPC
* by default, build runs outside VPC
* it cannot access resources in VPC
* you can specify VPC
    * VPC ID    
    * subnet
    * security group
* then build can access in your VPC resources

