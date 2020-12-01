### Q1
An organization's application needs to monitor application specific events with a standard AWS service.  
The service capture the number of logged in users and trigger events accordingly. During peak times, monitoring frequency will occur every 10 seconds.  
What should be done to meet these requirements? 
* Create an Amazon SNS notification
* Create standard resolution custom Amazon CloudWatch log
* **Create a high-resolution custom Amazon CloudWatch metric**
* Create a custom Amazon CloudTrail log   
    * when creating an alarm, select a period that is greater or equal to the frequency of the metric to be monitored. For example, basic monitoring for Amazon EC2 provides metrics for your instances every 5 minutes. When setting an alarm on a basic monitoring metric, select a period of at least 300 seconds (5 mins).  
    Detailed monitoring for EC2 provied metrics for your instances every 1 minute. When setting an alarm on a detailed monitoring metric, select a period of at least 60 seconds (1 min)
    * if you set an alarm on a high-resolution metric, you can specify a high-resolution alarm with a period of 10 seconds or 30 seconds, or you can set a regular alarm with a period of any multiple of 60 seconds 
    * https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html

