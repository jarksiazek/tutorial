### Synchronous Invocations
![](images/aim1.jpg)
* CLI, SDK, Gateway, ALB
    * result is returned right way 
    * error handling must happen client side (reties, exponential backoff, etc)

### Synchronous Invocations - Services
* user invoked 
    * ALB
    * API Gateway
    * CloudFront (Lambda@Edge)
    * S3 Batch 
* service invoked
    * Cognito
     * AWS Step Functions
* Other services
    * Amazon Lex, Alexa. Kinesis Data Firehose