### Lambda Execution Roles
* grants the Lambda function permissions to AWS services/resources
* sample managed policy for Lambda
    * AWSLambdaBasicExecutionRole - Upload logs to CloudWatch
    * AWSLambdaKinsisExecutionRole - Read from Kinesis
    * AWSLambdaDynamoDBExecutionRole - Read from DynamoDB
    * etc
* whenever you use an event source mapping to invoke your function, Lambda uses the execution role to read event data
* best practice is to create one Lambda Execution Role per function    
    
### Lambda is invoked by other services
* use **resource based policy**
* gives other account and AWS services permission to use your Lambda resources
* similar to S3 bucket policies for S3 bucket
* an IAM principal can access Lambda
    * if the IAM policy attached to the principal authorizes it (e.g. user access)
    * OR if the resource-based policy authorizes (e.g. service access)
* when an AWS service like Amazon S3 calls your Lambda function, the resource-based policy gives it access
