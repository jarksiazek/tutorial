### EFS ###
* Elastic File System
* managed NFS (network file system) that can be mounted on many EC2
* works with multi AZ's 
* locked in one region
* highly available, scalable, expensive 3x gp2, pay per use
* use cases: content management, wer serving, data sharing, Wordpress
* uses NFSv4.1 protocol
* uses security group to control access to EFS
* only on linux based on AMI (not Windows)
* encryption at rest using KMS
* POSIX file system (~Linux) that has a standard file API
* EFS Scale 
    * 1000s of concurrent NFS clients, 10GB+ /s throughput
    * grow to petabyte-scale network file system, automatically
* Performance mode (set at EFS creation time)
    * General purpose(default), latency-sensitive use cases (web server, CMS)
    * Max I/O - higher latency, throughput, highly parallel (big data, media processing)
* Storage Tiers (lifecycles management feature - move file after N days)
    * Standard: for frequently accessed files
    * Infrequent access (EFS-IA): cost to retrieve files, low price to store
    
 ### Create  EFS ###
 * create efs and connect 1 EFS to 2 EC2's  
 https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19733800#content
