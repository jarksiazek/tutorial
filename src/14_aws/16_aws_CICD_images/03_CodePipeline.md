### AWS CodePipeline ###
* continuous delivery
* visual workflow
* orchestration
    * source: GitHub/CodeCommit/S3
    * build: CodeBuild/Jenkins/etc
    * load testing: 3rd party 
    * deploy: AWS CodeDeploy/ Beanstalk/ CloudFormation/ ECS
    
    
### AWS CodePipeline Stages ###
* each stage can have sequential actions and/or parallel actions
* stages examples: Build/Test/Deploy/ Load Test/ect...
* manual approval can be defined at any stage


## AWS CodePipeLine Artifacts
![](images/aim1.jpg)
* each pipeline stage can create artifacts
* artifacts are passed stored in S3 and passed on the next stage

## AWS CodePipeLine Troubleshooting
* CodePipeline state changes happen in AWS CloudWatch Events, which can in return create SNS notification
    * e.g. can create events for failed pipelines
    * e.g. can create events for cancelled stages
* If CodePipeline fails a stage, your pipeline stops and you can get information in the console
* AWS CloudTrail can be used to audit AWS API calls    
* If Pipeline can't perform an action, make sure the "IAM Service Role" 
                     