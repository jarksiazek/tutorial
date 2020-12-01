### DynamoDB Write Sharding
![](images/aim6.jpg)
* imagine we have a voting application with two candidates, candidate A and candidate B
* if we use a partition ket of candidate_id, we will run into portions issues, as we only have two partitions 
* solution: add a suffix (usually random suffix, sometimes calculated suffix)





