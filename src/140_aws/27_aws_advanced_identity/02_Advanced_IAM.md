### Advanced IAM - making decision to allow or deny ###
1. If there is an explicit DENY, end decision is DENY
2. If there is an ALLOW, end decision is ALLOW
3. else DENY

### IAM Policies and S3 Bucket Policies ###
* IAM Policies are attached to users, roles, groups
* S3 Bucket Policies are attached to buckets 
* when evaluating if an IAM Principal can perform an operation X on a bucket, the union of its assigned IAM Policies and S3 Bucket Policies will be evaluated
* example 1 
    * IAM Role attached to EC2 instance, authorizes Read/Write to "my_bucket"
    * No S3 Bucket Policy attached
    * => EC2 instance can read and write to "my_bucket"
* example 2 
    * IAM Role attached to EC2 instance, authorizes Read/Write to "my_bucket"
    * S3 Bucket Policy explicit deny to the IAM Role 
    * => EC2 instance cannot read and write to "my_bucket"          
* example 3 
    * IAM Role attached to EC2 instance, no S3 bucket permissions
    * S3 Bucket Policy explicit read/write to the IAM Role
    * => EC2 instance can read and write to "my_bucket"      
* example 4 
    * IAM Role attached to EC2 instance, explicit deny s# bucket permissions
    * S3 Bucket Policy explicit read/write to the IAM Role
    * => EC2 instance cannot read and write to "my_bucket"        
    
### Dynamic Policies with IAM ###
* how do you assign each user a */home/user* folder in an S3 bucket? 
* option 1 - one IAM policy per user
    * create an IAM policy allowing Mike to have access to */home/mike*
    * create an IAM policy allowing Sarah to have access to */home/sarah*
* option 2 - dynamic policy with IAM
    * leverage the special policy variable ${aws:username}
    ![](images/aim4.jpg)
    
### Inline and Managed Policies ###
* AWS Managed Policy
    * Maintained by AWS 
    * Good for power users and administrators
    * updated in case of new services/ new APIs
* Custom Managed Policy
    * best practice, re-usable, can be applied to many principals
    * version controlled + rollback, central change management
* Inline 
    * strict one-to-one relationship between policy and principal
    * policy is deleted if you delete the IAM principal    

    
     
    