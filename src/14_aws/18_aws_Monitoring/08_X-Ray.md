### X-Ray
* Visual analysis of your application
* recommended specially for microservices
* Easy to troubleshooting performance
* Understand dependencies in a microservice architecture
* Pinpoint request behaviour
* Find errors and exceptions
* Are we meeting time SLA
* Identifying users that are impacted

### X-Ray Compatibility
* AWS Lambda
* Elastic Beanstalk
* ECS
* ELB
* API Gateway
* EC2 instances or any applications (even on premise)

### X-Ray Tracing
* Tracing is an end to end way to following a "request"
* each component dealing with the request adds its own "trace"
* Tracing is made of segments (+sub segments)
* Annotations can be added to traces to provide extra-information
* Ability to trace:
    * every request
    * sample request (as a % for example or a rate per minute)
* X-ray security
    * IAM for authorization
    * KMS for encryption at rest

### X-Ray How to enable?
1. Your code (Java, Python, Go, Node.js, NET) must import the AWS X-Ray SDK 
    * very small code modification needed
    * the application SDK will then capture: 
        * Calls to AWS services
        * HTTP/HTTPS requests
        * Database calls (MySQL, PostgreSQL, DynamoDB)
        * Queue calls (SQS)
2. Install the X-ray daemon or enable X-Ray AWS Integration
    * X-ray daemon works as a low level UDP packet interceptor (Linux/Win/Mac)
    * AWS Lambda/other AWS services already run the X-Ray daemon for you
    * Each application must have the IAM right to write data on X-ray

### X-Ray troubleshooting
* If X-ray not working on EC2
    * Ensure the EC2 Role has proper permissions
    * Ensure the EC2 instance is running the X-ray Daemon
* To enable on Lambda 
    * ensure it has an IAM execution role with proper policy (AWSX_RayWriteOnlyAccess)
    * ensure that X-Ray is imported in the code
    
### X-Ray instrumentation
* Instrumentation means the measure of product's performance, diagnose errors, and to write trace information
* to instrument your application code, use the X-Ray SDK
* many SDK require only configuration changes 
* you can modify your application code to customize and annotation the data that the SDK sends to X-ray, using interceptors, filters, middleware 

### X-Ray concept
* segments: each application/service will send them 
* subsegments: if you need more details in your segment
* trace: segments collected together to form an end-to-end trace
* sampling: decrease te amount of request sent to X-ray, reduce cost
* annotations: key value pairs used to index traces and use with filters
* metadata: key value pairs, not indexed, not used for searching

### X-Ray sampling
* default rules
    * control the amount of data that you record
    * you can modify sampling rules without changing the code
    * by default, the X-ray SDK records the first request each second, and five percent of additional requests
    * one request per second is the reservoir, which ensures that at least one trace is recorded each second as long as the service is serving requests
    * five percent is the rate at which additional requests beyond the reservoir size are sampled
* Custom sampling rules
    * rules for a reservoir and rate
    * we can add more data or reduce
    * max is reservoir = 1 and rate = 1
    
### X-Ray API, rights
* Write Policy
    * PutTraceSegments: upload segment document to AWS X-Ray
    * PutTelemetryRecords: used by AWS, X-Ray records to upload telemetry
        * Segments received, rejected, backendConnectionErrors
    * GetSamplingRules: retrieving all segment rules
    * GetSamplingStatisticSummaries: advanced
* Read policy
    * GetServiceGraph - main graph
    * BatchGetTraces - batch traces collections of segment documents
    * GetTraceSummaries - retrieves IDs and annotations for traces available for a specified time
    * GetTraceGraph - retrieves a service graph for one or more specific traces

### X-Ray with Beanstalk
* AWS Beanstalk includes the X-ray - daemon installed
* you can run daemon by setting an option or configure .ebextension/xray-daemon.config
* make sure to give your instance profile the correct IAM 
* make sure that your application code is instrumented with SDK X-ray
* X-ray daemon is not provided for multicontainer docker

### X-Ray with ECS
* X-ray container as daemon - ECS Cluster
    * if you run 10 EC2 you need to have 10 x-ray daemons - one per container
* X-Ray container as a "Side Car" - ECS Cluster
    * one application in EC2 needs one x-ray daemon - 
* X-Ray container as a "Side Car" - Fargate
    * x-ray per application - app container
      