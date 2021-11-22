### Q1
You are working on a new project involving creation of Lambda function for a Serverless Web App. A large team of developers are going to work on this project performing multiple changes to the ALmbda fucntion code. 
As a best practice, you have been asked to publish a version while creating Lambda function or updating a function code. 
Which of the following is TRUE with regards to the published version of a Lambda Function?
* a published version is a snapshot of function code and has the same version number when a previous version is deleted and recreated
* a published version is a snapshot of function code and has a unique Amazon Resource Name (ARN) whci hcan bve updated by using "UpdateFunctionCode"
* a published version is a snapshot of function code and configuration that can be updated using "Publish" parameter
* **a published version is a snapshot of function code and configuration tah can't be changed**
    * a published version copy of Lambda code and configuration $LATEST version. Con configuration can be done to publish a version and has a unique ARN which cannot be modified.
    * https://docs.aws.amazon.com/lambda/latest/dg/configuration-versions.html

### Q2
You have a number of Lambdas that need to deployed using AWS CodeDeploy. The Lambdas gone through multiple code revisions and versioning in Lambda is being used to maintain the revisions.  
Which of the folloing mnust be done ensure that the right version of the function is deployed in AWS CodeDeploy? 
* **Specify the version to be deployed in the AppSpec file**
    * https://docs.aws.amazon.com/codedeploy/latest/userguide/application-specification-files.html
    * the AppSpec file can be formatted with either YAML or JSON. It can also be typed directly into an editor in the console.
    * the AppSpec file is used to specify:
        * the AWS Lambda function version to deploy
        * the functions to be used as validation tests    
* Specify the version to be deployed in the BuildSpec file
* Create a Lambda environment variable called "VER" and mention the version that need to be deployed
* Create an ALIAS for the Lambda function. Mark this as the recent version. Use this ALIAS in CodeDeploy. 
 
