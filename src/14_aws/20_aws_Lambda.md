### Serverless ###
* developers don't have to manage servers
* serverless == function as a Service (FaaS)
* started from Lambda, but now is also database, messaging, storage, etc
* Servless in AWS
    * AWS Lambda
    * DynamoDB
    * AWS Cognito
    * AWS API Gateway
    * Amazon S3
    * AWS SNS & SQS
    * AWS Kinesis Data Firehose
    * Aurora Serverless
    * Step Function 
    * Fargate

### AWS Lambda
* virtual function - no server to manage
* limited by time - short executions
* run on-demand
* scaling is automated

### AWS Benefits
* easy pricing: 
    * pay per request and compute time
    * free tier 1 mln AWS lambda requests or 400000 GBs of compute time (400000 seconds with 1GB RAM)
    * after free tier $0.20 per 1mln requests
    * pay per duration (increment every 100 ms)
    * after free tier 1$ per 600000 GBs
* easy integration with whole AWS suite of services
* integrated with many languages
* easy monitoring through AWS CloudWatch
* easy to get more resources per function (up to 3 GB of RAM)
* increasing RAM will also improve CPU and network

### AWS Languages
* Node.js
* Python 
* Java
* C# (.Net)
* Golang
* C# / powershell
* Ruby
* Custom Runtime API ( community supported, example Rust)
* Important: Docker is not for AWS Lambda, it's for ECS/Fargate

### AWS Lambda Integrations
* API Gateway - create REST API
* Kinesis 
* DynamoDB - can trigger lambda functions
* Amazon S3 - can trigger lambda functions
* CloudFront - 
* CloudWatch Events/Event Bridge
* CloudWatch Logs
* SNS - to react on notification topics
* SQS - process messages 
* Cognito - react on action eg. when user logged in

### AWS Lambda Synchronous Invocations
* CLI, SDK, Gateway, ALB
    * result is returned right way 
    * error handling must happen client side (reties, exponential backoff, etc)
    * examples
        * user invoked 
            * CloudFront (Lambda@Edge), S3 Batch 
        * service invoked
            * Cognito, AWS Step Functions
        * Other services
            * Amazon Lex, Alexa. Kinesis Data Firehose

### AWS Lambda ALB
* Client -> ALB ( or API Gateway) -> Target Group 
* ALB to Lambda: HTTP to Json -> Json to HTTP
* ALB can support multi header values (ALB settings)

### AWS Lambda@Edge
* you have deployed a CDN using CloudFront
* global using AWS Lambda
* implement filtering before reaching your application 
* Lambda@Edge: 
    * deploying function alongside your CloudFront CDN
    * change CloudFront requests and responses
        * after CloudFront receives a request from viewer
        * before CloudFront forwards the request to the origin request
        * after CloudFront receives the response from the origin
        * before CloudFront forwards the reponse to the viewer 
    * use case
        * website security and Privacy
        * Dynamic Web Application at the Edge
        * SEO
        * Intelligently Route Across Origins and Data Center
        * Bot Mitigation at the Edge
        * Real time image transformation 
        * A/B Testing
        * User authentication and authorization
        * user prioritization
        * user tracking and analytics 

### Lambda Async
* S3, SNS, CloudWatch, Events/ Event Bridge
* the events are placed in an Event Queue
* lambda attempt to retry on errors
    * 3 tries total 
    * second attempt will start after 1 min, 3rd 2 min after 2nd attempt
* make sure that your process is idempotent (in case of retries)
* if the function is retried you will see duplicate logs entries in CloudWatch Logs
* can define DLQ (Dead letter Queue)           
        
### Lambda Event/Bridge Events
* invoke using cli 
* do not wait for results

### Lambda S3 Event Notifications
* trigger lambda function on (creating, removing, restoring, replication)
![](.20_aws_Lambda_images/aim1.jpg)
S3 bucket new event -> Lambda 
- send Matadata to RDS
- send Metadata to DynamoDB

### Event Source Mapping
* Sources
    * Kinesis Data Streams
    * SQS & SQS FIFO queue
    * DynamoDB Streams
* Records need to be polled from the source
* your Lambda function is invoked synchronously

### Lambda Destinations
* sending results of asynchronous invocations or the failures somewhere 
    * SQS, SNS, AWS Lambda, EventBridge bus
    * user destinations instead of DLQ(can be used in same time)
* event source mapping 
    * discarded event batches
    * SQS, SNS
    * can use DQL as well 
    
### Lambda Execution Roles 
* IAM must be attached to lambda
* create one lambda execution role per function
* when lambda is invoked by other service, use Lambda Based Policies
    * 

  
