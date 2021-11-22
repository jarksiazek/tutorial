### Q1
Set up the read and write throughput for table. Data is going to be read at  the rate of 3000 items every 30 seconds. Each item is of 6 kb. The reads can be eventual consistent reads.   
What should be the read capacity that needs to be set? 
* **10**
    * https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html
    * 300/30 = 10 items every second
    * 2 eventually reads per second with size 4 kb
    * 6 kb = 2 reads required
    * 10 * 2 = 20    
* 20 
* 6 
* 30

### Q2
Company is writing 10 items to the Dynamo DB every second. Each is 15.5 kb. 
What would be the required provisioned write throughput for the best performance?
* 10
* **160** 
    * 10 * 16 = 160
* 155 
* 16