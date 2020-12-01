### Q1
As developer, you need to ensure the right services are used during development and subsequent deployment of the application.   
Which of the following would  you consider incorporating to ensure **loaderboards** can be maintained accurately in the application?
* Beanstalk
* **ElasticCache - Redis**
    * Gaming Leaderboards (Redis Sorted Sets)
    * LeaderBoards - such as the Top 10 scores for a game, are computationally complex, especially with a large number of concurrent players and continually changing scores. 
    Redis sorted sets guarantee both uniqueness and element ordering. Using Redis sorted sets, each time a new element is added to the sorted set, it's reranked in real time. 
* ElasticCache - Memcaches
* AWS Opswork

### Q2
You are developing an application that is going to make use of Amazon Kinesis. Due to the high throughput, you decide to have multiple shards for streams.  
Which of the following is TRUE when it comes to processing data across multiple shards? 
* **You cannot guarantee the order of data across multiple shards. Its possible only within a shard**
    * https://aws.amazon.com/blogs/database/how-to-perform-ordered-data-replication-between-applications-by-using-amazon-dynamodb-streams/
* Order of data is possible across all shards in a stream
* Order of data is no possible across at all in Kinesis streams
* You need to use Kinesis firehose to guarantee the order of data 
