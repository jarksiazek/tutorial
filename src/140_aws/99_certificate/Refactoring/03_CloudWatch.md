### Q1
An app is publishing a custom CloudWatch metric any time an HTTP 504 error appears in the app error logs. These errors are being received intermittently. There is a CloudWatch Alarm for this metric and Developer would like the alarm to trigger ONLY if it breaches two evaluation periods or more.  
What should be done to meet these requirements ?
* Update the CloudWatch Alarm to send a custom notification depending on results
* Publish the value zero whenever there are on "HTTP 504" errors
* Use high-resolution metrics to get data pushed to CloudWatch more frequently
* **the evaluation period and Data Points to Alarm should be set 2 while creating this alarm**
    * when you create an alrm, you specify three setting to enable CloudWatch to evaluate when to change the alarm state
        * **Period** this length of time to evaluate the metric to create each individual data point for a metric. if oyu choose one minute as the period, there is one datapoint every minute
        * **Evaluation Period** is the number of the most recent data points to evaluate when determining state
        * **Datapoints to Alarm** is the number of data points within the evaluation period that must be breaching to cause the alarm to go to ALARM state. The breaching data points do not have to be consecutive, they just must all be withing the last number of data points equal to Evaluation.
        * https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch-Agent-common-scenarios.html#CloudWatch-Agent-aggregating-metrics
        
  
 