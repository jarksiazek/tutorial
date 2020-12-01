### Lambda Logging and Monitoring ###
* CloudWatch Logs: 
    * AWS Lambda execution logs are stored in AWS CloudWatch Logs 
    * make sure your AWS Lambda function has ab execution role with an IAM policy that authorizes writes to CLoudWatch Logs 

* CloudWatch Metrics:
    * AWS Lambda metrics are displayed in AWS CloudWatch Metrics
    * Invocations, Durations, Current Executions
    * Error count, Success Rates, Throttles
    * Async Delivery Failures
    * Iterator Age (Kinesis, DynamoDB Streams)
    
* Tracing with X-Ray:
    * enable in Lambda configuration (Active Tracing)
    * runs the X-Ray daemon for you
    * use AWS X-Ray SDK in Code
    * ensure Lambda Function has a correct IAM Execution Role
        * managed policy is called AWSXRayDaemonWriteAccess
    * environment variables to communicate with X-Ray
        * _X_AMZN_TRACE_ID: contains the tracing header   
        * AWS_XRAY_CONTEXT_MISSING: by default, LOG_ERROR   
        * AWS_XRAY_DAEMON_ADDRESS: the X-Ray Daemon IP_ADDRESS:PORT   
