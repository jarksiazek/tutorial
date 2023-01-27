### CloudWatch
* All services
  * every service
  * belong to namespaces
  * dimension - an attribute of a metric (instance id, env, etc)
  * 10 dimensions per metric
* EC2
  * standard monitoring (above list)
    * every 5 mins 
  * detailed monitoring
    * every 1 min
    * free tier 10 detailed monitorings 
    * memory usage is not pushed
  * custom metrics
    * eg. RAM, disk space, number of logged in users..
    * API call PutMetricData
    * ability to use dimensions(attributes) to segment metrics
      * instance id
      * environment.name
    * resolution
      * standard - 1 min
      * high resolution - 1/5/10/30 sec - higher cost
      * accecpt data points two weeks in the past and 2 hours in the future 
### Logs
* Log groups - arbitrary name (eg. an app name)
* Log stream - instances within application/ log files/ containers
* log expiration policy 
* can be sent to: S3, Kinesis Data Streams/Firehose, Lambda, ElasticSearch
* Sources
  * SDK, CloudWatch Logs Agent, CloudWatch Unifed Agent
  * Elastic Beanstalk 
  * ECS: logs from contrainers
  * AWS lambda: function logs
  * VPC flow logs 
  * API Gateway
  * Cloudtrail
  * Route53: Log DNS queries
* Metric Filter & Insight
  * filter expressions
    * eg. speficic IP
* metrics from logs can be used to trigger CloudWatch alarms
* Cloudwatch logs insight queries logs and adds them to CloudWatch Dashboards
* Logs aggregation
  * cloudwatch logs -> subscription filter -> kinesis data streams -> s3

### Alarms
* States: OK, INSUFFICIENT_DATA, ALARM
* Period: 
  * low and high resolution(custom metrics)
* Targets
  * EC2 - Stop, Terminate Reboot, Recover
  * EC2 Auto Scaling action - up and down
  * SNS
* Composite alarms - multi alarms monitoring

### AWS Config
* per region service
* auditing and recording compliance
* record configurations
* helps with:
  * unrestricted SSH access 
  * buckets have public access
  * changing ALB configuration 
