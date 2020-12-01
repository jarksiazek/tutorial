### Q1
You are using Cognito identity pools to assign authenticated SAML users a temporary access for downloading data from S3. For this you have created multiple rules for each role which gets assigned to users. 
Which of the following criteria is matched for evaluating these rules?
* Rules are evaluated in sequential order and rule with lower value is preferred  
* Rules are evaluated in sequential order and IAM role for fisrt matching rule is used unless a standard attribute is specified to override the order  
* Rules are evaluated in sequential order and rule with higher value is preferred  
* **Rules are evaluated in sequential order and IAM role for first matching rule is used unless a CustomRoleArn is specified to override the order**
