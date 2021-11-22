### Event Source Mapping
![](images/aim16.jpg)
* Sources
    * Kinesis Data Streams
    * SQS & SQS FIFO queue
    * DynamoDB Streams
* Records need to be polled from the source
* your Lambda function is invoked synchronously

### Event Source Mapping Categories
* Streams
    * Kinesis and DynamoDB
    * event source mapping creates an iterator for each shard, process items in order
    * start with new items, from the beginning or from timestamp
    * processed items aren't removed from the stream (other consumers can read them)
    * use cases:
        * low traffic: use batch window to accumulate records before processing
        ![](images/aim17.jpg)
    * Error Handling
        * function return an error, entire batch reprocessed until the function succeeds, or the items in the batch expire
* Queues
    * SQS and SQS FIFO
        ![](images/aim18.jpg)
        * event Source Mapping will poll SQS (Long Polling)
        * batch size 1-10
        * use a DLQ (on SQS)      
