### AWS CloudWatch Logs Events
* Schedule: CRON jobs
* Event pattern: Event rules to react to a service doing something
    * e.g. CodePipeline was changed 
* Can trigger Lambda function, SQS/SNS 
* When triggered, CloudWatch Event creates small JSON to give your more information
      