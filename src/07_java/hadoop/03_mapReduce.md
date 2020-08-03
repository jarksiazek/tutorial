### MapReduce ###
MapReduce
* programming paradigm
* designed to solve one problem
* created by Google
* 2 parts 
    * map 
        * some actions on some data 
        * execute on each node
    * reduce 
        * reduce function
        * execute only on some node
        * aggregate sets of <key, value> pairs 
        * output a combined list
    
MapReduce 1.0
* distributed, scalable, cheap
* Storage 
    * HDFS - triple replicated
    * commodity hardware
* parallel via Map(local) and Reduce (aggregated) 

MapReducer Example 
```java
public class MapReduce {
    public static void main(String[] args){
      //create JobRunnerInstance
      //call MapInstance on JobInstance
      //call ReduceInstance on JobInstance
    }
    public void Map() {
        //write Mapper
    }
    public void Reduce() {
       //write Reducer
    } 
}
```