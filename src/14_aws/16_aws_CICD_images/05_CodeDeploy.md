### AWS CodeDeploy ###
* deploy application automatically to many EC2 instances
* these instances are not managed by Elastic Beanstalk 
* there are several ways to handle deployment using open source tools (Ansible, Terraform, Chef, Puppet, etc)
* AWS Deploy - managed service

### AWS CodeDeploy - Steps ###
* Each EC2 Machine (or On Premise machine) must be running the CodeDeploy Agent
* the agent is continuously polling AWS CodeDeploy for work to do
* CodeDeploy sends **appspec.yml** file
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