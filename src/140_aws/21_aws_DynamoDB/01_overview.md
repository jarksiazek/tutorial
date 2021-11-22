### NoSQL ###
* are non-relational databases and are distributed
* not supported **join**  
* all the data that is needed for a query is present in one row
* do not supported **aggregations such as "SUM"**
* databases are scale horizontally

### DynamoDB
![](images/aim14.jpg)
* fully managed, highly available with replication across 3 AZ
* scales to massive workload, distributed database
* millions of requests per second, trillions of row, 100s of TB of storage
* fast and consistent in performance (low latency on retrieval)
* integrated with IAM for security, authorization and administration
* enables event driven programming with **DynamoDB Streams**
* low cost and auto scaling capabilities

### DynamoDB Basics
* DynamoDB is made of tables
* each table has a **primary key** (must be decided at creation time)
* each table can have an infinite number of items (=rows)
* each item has **attributes** (can be added over time - can be null)
* max size of item is 400kb
* data types supported are:
    * scalar types: String, Number, Binary, Boolean, Null
    * document types: List, Map
    * set types: String set, Number set, Binary Set

### DynamoDB PrimaryKey
* Option 1: Partition key only (hash)
![](images/aim1.jpg)
    * partition key must be unique for each item
    * partition key must be "diverse" so that the data is distributed
    * example: user_id for users table 

* Option 2: Partition key + Sort key
![](images/aim2.jpg)
    * the combination must be unique
    * data is grouped by partition key
    * sort key == range key
    * example: users-games table
        * user_id - partition key
        * game_id - sort key

