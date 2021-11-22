### Asynchronous Invocations
![](images/aim12.jpg)
* S3, SNS, CloudWatch, Events/ Event Bridge
* the events are placed in an **Event Queue**
* lambda attempt to retry on errors
    * 3 tries total 
    * second attempt will start after 1 min, 3rd 2 min after 2nd attempt
* make sure that your process is **idempotent** (in case of retries)
* if the function is retried you will see **duplicate logs entries in CloudWatch Logs**
* can define DLQ (Dead letter Queue)     

### Asynchronous Invocations - Services
* S3
* SNS
* CloudWatch Events / Event Bridge
* Code Commit
* Code Pipeline
* CloudWatch Logs
* Simple Email Service
* CloudFormation
* AWS Config
* AWS IoT
* AWS IoT Events 