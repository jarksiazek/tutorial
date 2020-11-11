### CICD ###
* AWS CodeCommit: storing our code
* AWS CodePipeline: automating our pipeline from code to ElasticBeanstalk
* AWS CodeBuild: building and testing our code
* AWS CodeDeploy: deploying the code to EC2 fleets (not Beanstalk)

### Technology Stack CICD ###
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

### AWS CodeCommit ###
* version control on central online repository
* private GIT repositories
* no size limit on repositories (scale seamlessly)
* code only in AWS Cloud account => increase security and compliance
* secure (encrypted, access control, etc) 
    * integration are done using Git (standard)
    * authentication 
        * SSH Key: AWS Users can configure SSH keys in their IAM Console
        * HTTPS: Done through the AWS CLI Authentication helper or Generating HTTPS credentials
        * MFA (multi factor authentication) can be enabled for extra safety
    * authorization
        * IAM Policies manage user/ roles rights to repositories
    * encryption:
        * Repositories are automatically encrypted at rest using KMS
        * encrypted in transit (can only use HTTPS or SSH - both secure)  
    * cross account access: 
        * do not share SSH keys
        * do not share AWS credentials
        * use IAM Role in your AWS Account and use AWS STS (with AssumeRole API)
* CodeCommit vs GitHub
    * similarities
        * both are git repositories
        * support code review
        * integrate with CodeBuild
        * support HTTPS and SSH
    * differences
        * security
            * GitHub: GitHub Users
            * CodeCommit: AWS IAM users & roles
        * hosted
            * GitHub: hosted by GitHub
            * GitHub Enterprise: self hosted by organization
            * CodeCommit: managed and hosted by AWS
        * UI
            * GitHub: UI is fully GitHub Users
            * CodeCommit: UI is minimal
* CodeCommit Notifications
    * AWS SNS (Simple Notification Service) or AWS Lambda or AWS CloudWatch Event Rules
    * Notification types SNS/AWS Lambda:
        * deletion of branches
        * trigger for pushes that happens in master branch
        * notify external Build System
        * trigger AWS Lambda function to perform codebase analysis (maybe credentials got committed in the code?)
    * Notification types CloudWatch Evetn Rules:
        * Trigger for pull request updates (created/updated/deleted/commented)
        * Commit comment events
        * CloudWatch Event Rules triggers SNS topic  
 
### AWS CodePipeline ###
* continuous delivery
* visual workflow
* orchestration
    * source: GitHub/CodeCommit/S3
    * build: CodeBuild/Jenkins/etc
    * load testing: 3rd party 
    * deploy: AWS CodeDeploy/ Beanstalk/ CloudFormation/ ECS
* made of stages
    * each stage can have sequential actions and/or parallel actions
    * manual approval can be defined at any stage
* AWS CodePipeLine works on Artifacts
    * each pipeline stage can create artifacts
    * artifacts are passed stored in S3 and passed on the next stage
        ![](.16_aws_CICD_images/aim1.jpg)
* CodePipeline Troubleshooting
    * CodePipeline state changes happen in AWS CloudWatch Events, which can in return create SNS notification
        * e.g. can create events for failed pipelines
        * e.g. can create events for cancelled stages
    * If CodePipeline fails a stage, your pipeline stops and you can get information in the console
    * AWS CloudTrail can be used to audit AWS API calls    
    * If Pipeline can't perform an action, make sure the "IAM Service Role" 
                     
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
* CodeBuild supports:
    * Java, Ruby, Python, Go, Node.js, Android, .NET Core, PHP
    * Docker: extends any environment you like  
![](.16_aws_CICD_images/aim2.jpg)
* BuildSpec
    * buildspec.yml file must be at the root of the code
    * define environment variables:
        * plaintext variables
        * secure secrets: use SSM Parameter store
    * phases:
        * install: install dependencies you may need for your build
        * pre build: final command to execute before build
        * build: actual build commands
        * post build: finishing touches (zip out for example)
    * artifacts: what to upload to S3 (encrypted with KMS)
    * cache: files to cache (usually dependencies) to S3 for future build speedup
        
### AWS CodeDeploy ###
* deploy application automatically to many EC2 instances
* these instances are not managed by Elastic Beanstalk 
* there are several ways to handle deployment using open source tools (Ansible, Terraform, Chef, Puppet, etc)
* AWS Deploy - managed service

### AWS CodeDeploy - Steps ###
* Each EC2 Machine (or On Premise machine) must be running the CodeDeploy Agent
* the agent is continuously polling AWS CodeDeploy for work to do
* CodeDeploy sends appspec.yml file
* application is pulled from GitHub or S3
* EC2 will run the deployment instructions
* CodeDeploy Agent will report of success/failure of deployment on the instance

### AWS CodeDeploy - Primary Components ###
* Application - unique name
* Compute platform - EC2/On-Premise or Lambda
* Deployment configuration - deployment rules for success/ failures
    * EC2/On-Premise: you can specify the minimum number of healthy instances for deployment
    * AWS Lambda: specify how traffic is routed to your updated Lambda function versions
* Deployment group - group of tagged instances (allows to deploy gradually)    
* Deployment type - In-place deployment or blue/green deployment
* IAM instance profile - need to give EC2 the permissions to pull from S3/GitHub
* Application Revision - application code + appspec.yml file
* Service role - role for CodeDeploy to perform what it needs
* Target revision - target deployment application version 

### AWS CodeDeploy - AppSpec ###
* File section - how to source and copy from S3/ GitHub to filesystem
* Hooks - set of instructions to do to deploy the new version (hooks can have timeouts) 
    * ApplicationStop
    * DownloadBundle
    * BeforeInstall
    * AfterInstall
    * ApplicationStart
    * ValidateService - really important
    
### AWS CodeDeploy - Deployment Config ###
* Configs
    * One a time - one instance at a time, one instance fails => deployment stops
    * half at a time - 50% 
    * all at once - quick but no healthy host, downtime, good for dev
    * custom, min healthy host - 75% 
* Failures
    * instances stay in "failed state"
    * new deployments will first be deployed to "failed state" instances
    * to rollback - redeploy old deployment or enable automated rollback for failures
* Deployment Targets
    * Set of EC2 instances with tags
    * directly to an ASG  
    * Mix of ASG /Tags so you can build deployment segments
    * Customization in scripts with DEPLOYMENT_GROUP_NAME environment variables
     
 ### AWS CodeDeploy - Rollback ###
* automated rollback options
    * roll back when a deployment fails
    * roll back when alarm thresholds are met
    * disable rollbacks - do not perform rollbacks for this deployment
* if a roll back happens CodeDeploy redeploys the last known good  revision as a new deployment
    
 ### AWS CodeDeploy - CodeStar ###
* integrated solution that regroups GitHub, CodeCommit, CodeBuild, CodeDeploy, CodeFormation, CodePipeline, CloudWatch
* helps quickly create "CICD-ready" projects for EC2, Lambda, Beanstalk
* supports many language
* issue tracking JIRA/GitHub Issues
* Ability to integrate with Cloud9 to obtain a web IDE
* one dashboard to view all component
* service is free
* limited customization

    

     
