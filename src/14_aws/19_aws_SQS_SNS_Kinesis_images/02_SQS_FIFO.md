 ### Amazon SQS - FIFO ###
 ![](images/aim10.jpg)
* First In First Out
* limited throughput 300msg/sec without batching, 3000 msg/sec with batching
* exact one send capability (by removing duplicates)
* messages will be processed in order by consumer 

 ### Amazon SQS - Deduplication ###
* interval is 5 mins - if the same message will be sent twice in 5 minute period, the second one will be removed
* two de-duplication methods:
    * content-based deduplication - will do a SHA-256 hash of the message body  
    * explicitly provide a message duplication ID

 ### Amazon SQS - Message grouping
* if you specify the same value of MessageGroupId is SQS FIFO, you can only have one consumer
* to get ordering at the level of a subset of messages, specify different values for MessageGroupId
    * Message Group Id will be in order within the group
    * each Group Id will have different consumer (parallel processing)
    * ordering across groups in not guaranteed