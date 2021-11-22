### Amazon SNS + SQS - Fan out pattern ###
![](images/aim12.jpg)
* push one message in SNS, receive in all SQS queues that are subscribed
* full decoupled, no data loss
* SQS allows for: data persistence, delayed processing and retries of work
* ability to add more SQS subscribers over time
* make sure your SQS queue access policy allows for SNS to write
* **SNS cannot send messages to SQS FIFO (AWS limitation)**

### Amazon SNS + SQS - Fan out example ###
* S3 Events to multiple queues
    * for the same combination **event type + prefix** you can have only one S3 event rule
    * if you want ot send the same s3 event to many SQS queues, use **fan-out**
    ![](images/aim13.jpg)
    