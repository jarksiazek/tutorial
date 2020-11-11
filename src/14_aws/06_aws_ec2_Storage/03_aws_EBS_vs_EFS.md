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
 
