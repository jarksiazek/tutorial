### DynamoDB Streams
* changes on DynamoDB can end up in DynamoDB Stream
* this stream can be read by AWS Lambda or EC2
    * react to changes in the real time 
    * analytics
    * create derivative tables/views
    * insert data do ElasticSearch
    * 
 * could implement cross region replication using stream
 * stream has only 24 hours of data retention
 
### DynamoDB Streams - options
 * Data to be streamed
     * KEY_ONLY - only the key attributes of the modified item
     * NEW_IMAGE - the entire item as it appears after it was modified
     * OLD_IMAGE - the entire item as appeared before it was modified 
     * NEW_AND_OLD_IMAGE - both new and old image
* Streams are made of shards, just like Kinesis Data Streams
* DynamoDB shards are managed by AWS

### DynamoDB Streams and Lambda
![](images/aim5.jpg)
* need to define an Event Source Mapping to read from a DynamoDB Streams
* need to be ensure the Lambda function has the appropriate permissions
* Lambda function is invoked synchronously