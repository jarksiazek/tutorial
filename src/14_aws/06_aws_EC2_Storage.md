### EBS  ###
* attached network volume to EC2 (no a physical drive)
* EC2 can have more than one EBS or zero
* EBS - Elastic Block Store - is a network drive you can attach to your instance while they run
* it allows your instances to persist data
* can be detached from an EC2 and attached to another in one AZ
* locked to an AZ
    * An EBS Volume in us-east-1a cannot be attached to us-east-1b
    * to more a volume across, you first need to snapshot it
* Provisioned capacity (size GB, IOPS - input/output operations per second)
    * billed for all the provisioned capacity
    * capacity can be increased over time  
![](.06_aws_EC2_Storage_images/aim1.jpg) 

### EBS Volume Types ###
* Types
    * GP2 (SSD) - general purpose/ good balance price/performance
        * system boot value
        * virtual desktops
        * low-latency interactive apps
        * 1 to 16 GB
        * small GP2 volumes can burst IOPS to 3000
        * max IOPS is 16000
        * 3 IOPS per GB, means at 5333 GB we are at the max IOPS
        * Throughput is not applicable
    * IOI (SSD) - highest-performance, good for mission-critical low-latancy or high-throughput workloads
        * more than 16000 IOPS per volume 
        * Large database
        * MongoDB, Cassandra, PostgreSQL, Oracle ...
        * 1 GB to 16 TB
        * IOPS is provisioned (PIOPS) - min 100 - max 64000 (nitro instances) else max 32000 (other instances)    
        * 50 IOPS per GB
    * STI (HDD) - low cost HDD volume designed for frequently accessed 
        * streaming workload, fast throughput at low price
        * big data, data warehouses, log processing
        * appache kafka
        * cannot be a boot volume
        * 500 GB - 16TB
        * max IOPS is 500
        * max throughput of 500 MB/s - can burst        
    * SCI (HDD) - lowest cost HDD volume designed for infrequently accessed 
        * low cost
        * cannot be a boot volume
        * 500 GB - 16TB 
        * max IOPS is 250
        * max throughput of 250 MB/s - can burst 
* characteristics
    * size
    * throughput
    * IOPS - I/O per sec
* Only GP2 and IOI can be used as boot volumes


### Attached 2 EBS Volumes to EC2 ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19733746#content  
1.Create new EC2 instance  
2."Add storage" add second EBS volume  
3.Create instance

### Mount disk to EC2 ###
1.connect to instance using SSH
* all attached drives
```bash
$ lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0   8G  0 disk
└─xvda1 202:1    0   8G  0 part /
xvdb    202:16   0   2G  0 disk
```
* mounting second drive to EC2
    * determine whether to create file system on the volume
    ```bash
    $ sudo file -s /dev/xvdb
    /dev/xvdb: data
    ```
    * if "data" there is no file system, create one
    ```bash
    $ sudo mkfs -t ext4 /dev/xvdb
    ```
    * mount directory
    ```bash
    $ sudo mkdir /data
    $ sudo mount /dev/xvdb /data
    ```

### Instance store ###
* Some instances do not come with root EBS volumes
* they come with "Instance storage" (=ephemeral storage)
* instance store is physically attached to the machine
* up to 7.5 TB
* only specific instances have instance store 
* Prop:
    * Better I/O performance, very high IOPS max 1.6 milions
    * Good for buffer/cache/scratch data/ temporary content
    * data survives reboots
* Cons: 
    * On stop or termination, the instance store is lost
    * store size is fixed
    * backups must be operated by user
    
### EFS ###
* Elastic File System
* managed NFS (network file system) tah can be mounted on many EC2
* works with multi AZ's 
* locked in one region
* highly available, scalable, expensive 3x gp2, pay per use
* use cases: content management, wer serving, data sharing, Wordpress
* uses NFSv4.1 protocol
* uses security group to control access to EFS
* only on linux based on AMI (not Windows)
* Encryption at rest using KMS
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
 
 ### EBS vs EFS ###
 * EBS 
    * one instance at the time
    * locked to AZ
    * IO increases when the disk increases
    * to migrate data use snapshot and move it to other EBS
    * root volume will be terminated when EC2 gets terminated (default, can be disabled)
    * paid for provisioned size
 EFS
    * mounting of many instances across AZ
    * only linus - POSIX
    * more expensive than EBS
    * EFS-IA for saving cost
    * paid for actual size
 
