### Basic ###
Hadoop cluster 
* Open source 
    * Apache Hadoop
* Commercial Distribution
    * Cloudera, Hortonworks
* Public cloud 
    * IaaS - you install/manage (docker)
    * PaaS - vendor provides image and management

CAP Theory 
* consistency - very high consistency 
    * transactions 
* availability - have a copy of data 
* partitioning 
    * scalability

Hadoop 
* alternative file system HDFS
* HBase is noSQL database (wide columnstore)
* scalability (partitioning) 
    * commodity hardware for data storage
* flexibility (availability)
* not designed for transactions 

Kinds of data for hadoop
* Behavioral data
* LOB (Line of business)
  
Hadoop file system 
* HDSF Hadoop Distributed File System
* Regular file system 
* Cloud file system - similar to regular file system

Files and JVMs
* single node
    * local file system 
    * single JVM
* Pseudo-distributed node 
    * uses HDFS 
    * JVM deamons run processes

Hadoop ecosystem 
* 