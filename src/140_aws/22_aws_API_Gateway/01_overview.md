### Overview ###
* AWS Lambda + API Gateway: No infrastructure to manage
* support for WebSocket Protocol
* handle API versioning (v1, v2 ..)
* handle different environments (dev, test, prod...)
* handle security (Authentication and Authorization)
* create API keys, handle request throttling
* Swagger/ Open API import to quickly define APIs
* transform and validate requests and response
* generate SDK and API specification
* cache API responses

### API Gateway - integration high level
* Lambda Function
    * invoke Lambda
    * easy way to expose REST API backed by AWS Lambda
*  HTTP 
    * expose HTTP endpoints in the backend
    * example: internal HTTP API on premise, ALB ... 
    * Why? Add rate limiting, caching, user authentications, API keys, etc...
* AWS Service
    * expose any AWS API through the API Gateway
    * example: start an AWS Step Function workflow, post a message to SQS
    * Why? Add authentication, deploy publicly, rate control 
    
### API Gateway - endpoint types
* Edge-Optimized (default) - for global clients
    * requests are routed the CloudFront Edge locations (improves latency)
    * the API Gateway still lives in only one region
* Regional
    * for clients within the same region
    * could manually combine with CloudFront (more control over the caching strategies and the distribution)
* Private
    * can only by accessed from your VPC using an interface VPC (ENI)
    * use a resource policy to define access
    
     
