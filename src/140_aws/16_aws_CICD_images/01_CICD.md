### CICD ###
* AWS CodeCommit: storing our code
* AWS CodePipeline: automating our pipeline from code to ElasticBeanstalk
* AWS CodeBuild: building and testing our code
* AWS CodeDeploy: deploying the code to EC2 fleets (not Beanstalk)

### Continuous Integration
* Developers push the code to code repository
* Test/ build server checks the code as soon as it's pushed (CodeBuild/Jenkins)
* The developer test feedback about the test and checks that have passed/failed    
* Find bugs early, fix bugs

### Continuous Delivery
* ensure that the software can be released reliably whenever needed
* ensures deployments often an are quick

### Technology Stack CICD
![](images/aim3.jpg)
* Orchestrate: AWS CodePipeline
    * Code
        * AWS CodeCommit
        * GitHub 
    * Build 
        * AWS CodeBuild
        * Jenkins
    * Test 
        * AWS CodeBuild
        * Jenkins
    * Deploy 
        * AWS Elastic Beanstalk
        * User Managed EC2 Instances Fleet (AWS Code Deploy)
    * Provision
        * AWS Elastic Beanstalk
        * User Managed EC2 Instances Fleet (AWS Code Deploy)