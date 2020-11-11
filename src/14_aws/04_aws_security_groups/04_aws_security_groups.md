### Security Groups ###
* network security in AWS
* control traffic "firewall" into or out of our EC2 Machines
    * access to port
    * authorised IP ranges - IPv4 IPv6  
    
* can be attached to multi instances
* locked to a region /VPC combination 
* good practice - separate 
* "time out" - when application is not accessible
* "connection refused" - when application is not accessible
* all inbound traffic is blocked by default
* all outbound traffic is authorised by default


### Security Groups Settings ###
1. NETWORK & SECURITY -> Security Groups
2. Select security group 
3. Switch tab to "Inbound" - it controls traffic into EC2
    * type - shortcut to select most popular connection e.g. SSH
    * protocol
    * port range 
    * source 
        * anywhere 0.0.0.0/0 - all ip's are available
        *  
4. Switch tab to "Outbound" - it controls traffic from EC2

### IP Private vs Public ###
* IPv4 
    * IPv4 - 3.7 billion different addresses
    * IPv4 - [0-255].[0-255].[0-255].[0-255]

* Elastic Ip 
    * fix Ip 
    * public IPv4 you own as long as you don't delete it
    * can be attached to one instance at the time
    * 5 for one account
    * try to avoid it
    * use Load Balancer and do not use public IP