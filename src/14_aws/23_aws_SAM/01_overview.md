### Overview ###
* SAM - Serverless Application Model
* Framework for developing and deploying serverless applications
* All configuration is in YAML
* Generate complex CloudFormation from simple SAM YAML file
* Supports everything from CloudFormation
* only 2 commends to deploy to AWS
* SAM can use CodeDeploy to deploy Lambda function
* SAM can help you to run Lambda, API Gateway, DynamoDB locally 

### SAM Recipe ###
* transform header indicates it's SAM template:
    * *Transform: 'AWS::Serverless-2016-10-31'*
* write code 
    * *AWS::Serverless::Function* - Lambda
    * *AWS::Serverless::Api* - API Gateway
    * *AWS::Serverless::SimpleTable* - DynamoDB
* Package and deploy
    * *aws cloudformation package/ sam package*
    * *aws cloudformation deploy/ sam deploy*

### SAM Package and Deploy ###
![](images/aim1.jpg)

    