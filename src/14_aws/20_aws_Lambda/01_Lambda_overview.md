### Lambda Overview  ###
* virtual functions - no servers  to manage
* limited by time - short executions (max 15 mins)
* run on-demand
* scaling is automated

### Lambda Benefits  ###
* easy pricing
    * pay per request
* integrated with the whole AWS suite of services
* many programming languages
* easy monitoring through AWS CloudWatch
* easy to get more resources for functions (max 3 GB)
* increasing RAM will also improve CPU and network

### Lambda Integrations  ###
* API Gateway
* Kinesis
* DynamoDB - some changes can trigger lambda
* S3 - can trigger lambda
* CloudFront - Lambda@Edge
* CloudWatch Events/ Event Bridge
* CloudWatch Logs - to stream logs
* SNS
* SQS
* Cognito - ex. reacts when user log to database