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