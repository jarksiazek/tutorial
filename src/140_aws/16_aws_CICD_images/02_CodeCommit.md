### AWS CodeCommit ###
* version control on central online repository
* private GIT repositories
* no size limit on repositories (scale seamlessly)
* code only in AWS Cloud account => increase security and compliance

### AWS CodeCommit Security
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
    
### CodeCommit vs GitHub
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

### CodeCommit Notifications
* AWS SNS (Simple Notification Service) or AWS Lambda or AWS CloudWatch Event Rules
* Notification types SNS/AWS Lambda:
    * deletion of branches
    * trigger for pushes that happens in master branch
    * notify external Build System
    * trigger AWS Lambda function to perform codebase analysis (maybe credentials got committed in the code?)
* Notification types CloudWatch Event Rules:
    * Trigger for pull request updates (created/updated/deleted/commented)
    * Commit comment events
    * CloudWatch Event Rules triggers SNS topic  
