### AWS CloudWatch Logs
* application can send logs using SDK
* CloudWatch can collect data from: 
    * ElasticBeanstalk
    * ECS for containers
    * AWS Lambdas
    * VPC flow logs
    * API Gateway
    * CloudTrail based on filter
    * CloudWatch log agent: e.g. EC2 machine
    * Route53: Logs DNS queries
* Logs can be stored: 
    * S3 batch exporter for archival
    * Steam to ElasticSearch cluster
* Logs in CloudWatch
    * can use filter expression
    * log store architecture:
        * log groups: an arbitrary name, usually representing an application
        * log streams: instances within application/log files/containers
    * log expiration policy (never expire, 30 days, etc)
    * using the AWS CLI we can tail CloudWatch logs: 
    * Sending logs to CloudWatch be sure to have correct AIM permissions
    * Security: encryption of logs using KMS at the Group Level

### AWS CloudWatch Agent
* By default, no logs from EC2 will go to CloudWatch
* To store logs from EC2 you need to start CloudWatch agent (small program for sending logs)
* make sure AIM permissions are correct
* CloudWatch Logs Agent vs Unified Agent 
    * logs agent 
        * collect logs application (servers, on premises servers)
        * can send logs to CloudWatch Logs
    * unified agent
        * same as logs agent can do 
        * the new one version of agent 
        * can collect system-level metrics like RAM, CPU
        * Centralized configuration using SSM Parameter Store

### AWS CloudWatch Logs Metric Filter
* can use filter expression 
    * e.g. find a specific IP inside the logs
    * or count occurrences of "ERROR" in your logs
    * metric filters can be used for trigger alarm
* Filters only publish the metric data points for events that happen after the filter was created

### AWS CloudWatch Logs Events
* Schedule: CRON jobs
* Event pattern: Event rules to react to a service doing something
    * e.g. CodePipeline was changed 
* Can trigger Lambda function, SQS/SNS 
* When triggered, CloudWatch Event creates small JSON to give your more information
      