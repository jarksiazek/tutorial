### AWS CloudWatch Alarms
* useful for triggering notification for any metric
* use in Auto Scaling Group, EC2 Actions, SNS notifications
* various options (sampling, %, max, min, etc)
* alarm states: 
    * OK
    * INSUFFICIENT_DATA
    * ALARM
* Period 
    * Length of time in seconds to evaluate the metric
    * high resolution custom metric: can only by 10 sec or 30 sec