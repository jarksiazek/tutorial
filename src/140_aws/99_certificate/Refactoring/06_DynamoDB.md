### Q1
DynamoDB table has read throughput capacity of 5 RCU. Which of the following read configuration will provide us the max read throughput? 
* Read capacity set 5 for 4kb strong consistency
    * 5 * 4 * 2 = 40 
* Read capacity set 5 for 4kb eventual consistency
    * 5 * 4 = 20 
* Read capacity set 15 for 1kb strong consistency
* Read capacity set 5 for 1kb eventual consistency

### Q2
DynamoDB with a read capacity of 5 and a write capacity of 5.  
Which of the following statements are TRUE? (Select 3)
* **Strong consistent read of a max of 20 kb per second**   
    * 20/4 = 5
* Eventual consistent read of a max of 20 kb per second
* Strong consistent read of a max of 40 kb per second   
* **Eventual consistent read of a max of 40 kb per second**
    * 40/4/2 = 5
* **Max writes of 5 kb per second**
    * 5kb / 1 = 5