### Q1
a developer is writing several Lambdas that each access data in a commond RDS. They must share a connection string that contains the database credentials, which are a secret. A company policy requires that all secrets be stored encrypted.   
Which solution will minimize the amount of code?  
* Use commonn DynamoDB table to store setting
* Use AWS Lambda environment variables
* **Use System Manager Parameter store secure string**
    * System Manager Parameter Store provides secure, hierarchical storage for configuration
    * https://aws.amazon.com/blogs/compute/sharing-secrets-with-aws-lambda-using-aws-systems-manager-parameter-store/
* Use a  table in a separate RDS database

    