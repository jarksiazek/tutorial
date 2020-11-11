### Fundamentals ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/12203026#overview


### Regions ###
* blue - current, orange - soon  
* Names: us-east-1, eu-east-2  
* Regions - cluster of data centers   
https://aws.amazon.com/about-aws/global-infrastructure/regions_az/

### AWS Availability Zones ###
* each region has many zones: usually 3 per region, min 2, max 3
* AZ is one or more discrete data center with redundant power, networking, connectivity - are separate from each other
* they are connected with high bandwidth, ultra low latency networking
* example: 
    * Sydney: ap-southeast-2 - 3AZ
        * ap-southeast-2a
        * ap-southeast-2b
        * ap-southeast-2c

### IAM Introduction ###
* IAM - Identity and Access Management
* Users, Groups, Roles

![](.02_aws_fundamentals_images/aim1.jpg)

* ONE IAM User per person 
* ONE IAM Role per application

