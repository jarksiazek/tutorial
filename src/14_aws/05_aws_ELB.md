### Scalability ###
* application can handle greater loads by adapting
* 2 kinds of scalability
    * vertical
        * increasing size of the instance
        * good for database
        * hardware limits
    * horizontal - elasticity
        * increasing number of instances
* high availability
    * hand in hand with horizontal scaling
    * running your application/system in at least 2 data centers (2 AZs) 
    * goal is to survive a data center loss
    * passive 
        * RDS Multi AZ
    * active 
        * horizontal scaling    

### Load Balancing ###
* servers that forward traffic to multiple servers (EC2's) downstream
* single point of access (DNS)
* Seamlessly handle failures of downstream instances 
* Do regular health checks to your instances
* Provide SSL termination (HTTPS) for your websites
* Enforce stickiness with cookies
* High availability across zones
* Separate public traffic from private traffic

### EC2 Load Balancer ###
* ELB (EC2 Load Balancer) is a managed load balancer
    * AWS guarantees that will be working
    * AWS takes care of upgrades, maintenance, high availability
    * AWS provides only a few configuration knobs
    
### Health Checks ELB ###
* checks if the instance is good
* is done on a port and a route (/health is common)
* if the response is not 200, then the instance is unhealthy
* default is every 5 seconds

### Types of ELB ###
* classic load balancer (v1 - old generation) - 2009
    * HTTP(Layer 7), HTTPS(Layer 7), TCP(Layer 4)
    * health checks are TCP or HTTP based
    * fixed hostname XXX.region.elb.amazonaws.com
* application load balancer (v2 - new generation) - 2016
    * HTTP(Layer 7), HTTPS, WebSocket
    * HTTP/2 and WebSocket
    * load balancing to multiple HTTP applications across machines (target groups)
    * load balancing to multiple applications on the same machine (ex.containers)
    * routing tables to different target groups
        * based on url path 
            * /users -> go to one target group
            * /clients -> go to another target group
        * based on hostname in url
            * one.example.com -> go to one target group
            * two.example.com -> go to another target group
        * based on query strings, headers
            * one.example.com/users?id=123&order=false
    * great fit for micro services and container-based application (Docker, Amazon ECS)
    * port mapping feature to redirect to a dynamic port in ECS
    * target groups
        * EC2 instances (an Auto Scaling Group)
        * EC2 tasks (managed by ECS itself) - HTTP
        * Lambda functions - HTTP request is translated into a Json events
        * IP Addresses - must be private IPs
    * ALB can route to multiple target groups
    * Health checks are at the target group level
    * fixed hostname XXX.region.elb.amazonaws.com
    * the application servers don't see the IP of the clients directly
        * the true IP of the client is inserted in the header X-Forwarded-For
        * can also get Port (X-Forwarded-Port) and proto (X-Forwarded-Proto)
* network load balancer (v2 - new generation) - 2017
    * TCP, TLS(secure TCP), UDP
    * handle millions of request per second
    * Less latency ~100 ms (vs 400 ms for ALB)
    * exposes one static IP per AZ and supports assigning Elastic IP (helpful for whitelisting specific IP)
    * not for AWS free tier 
    
### Stickness ###
* redirection client always to the same instance
* works for Classic and Application Load Balancer
* The "cookie" used for stickness has an expiration date you control
* use case: make sure the user does not lose session data

### Cross-zone Load Balancing ###
* each load balancer instance distributes evenly across all registered instances in all AZ
* CLB
    * disable by default
    * No charges for inter AZ data if enabled
* ALB 
    * always on (can't be disable)
* NLB
    * disable by default
    * You pay charges ($) for inter AZ data if enabled

![](.05_aws_ELB_images/aim1.jpg) 

### SSL/TLS ###
* Basic
    * SSL Certificate allows traffic between your clients and your load balancer to be encrypted in transit (in-flight encryption)
    * SSL - Secure SocketsL Layer - encrypt connections
    * TLS - Transport Layer Security - new version of SSL
    * TLS are mainly used 
    * Public SSL certificates are issued by Certificate Authorities(CA)
* Load balancer 
    * uses an X.509 certificate (SSL/TLS server certificate)
    * you can manage certificates using ACM (AWS Certificate Manager)  
    * you can create upload your own certificates alternatively
    * HTTPS listeners: 
        * You must specify a default certificate
        * You can add an optional list of certs to support multiple domains
        * Clients can use SNI (Server )
    
![](.05_aws_ELB_images/aim2.jpg) 

* SNI - Server Name Indication
    * solve the problem of loading multiple SSL certificates onto one web server
    * newer protocol, requires the client to indicate the hostname of the target server in the initial SSL handshake 
    * only ALB & NLB, CloudFront
    
* Elastic Load Balancers - SSL Certificates
    * CLB
        * Supports only one SSL certificate
        * Must use multiple CLB for multiple hostname with multiple SSL certificates 
    * ALB and NLB
        * Supports multiple listeners with multiple SSL certificates 
        * Uses SNI to make it work
        
### ELB - Connection Draining ###
* Time to complete "in-flight requests" while the instance is de-registering on unhealthy
* Stop sending new requests to the instance which is de-registering
* Between 1 to 3600 seconds, default is 300 seconds 
* Can be disabled (set value to 0)
* Set to a low value if your requests are short
* Feature naming
    * CLB: Connection Draining 
    * Target Group (ALB and NLB) : Deregistration Delay
    
### ASG - Auto Scaling Group ###
* Basics
    * Scale out (add EC2) to match an increased load
    * Scale in (remove EC2) to match a decreased load
    * Ensure we have a minimum and a maximum number of machines running
    * automatically Register new instances to a load balancer
* Attributes 
    * Launch configuration
        * AMI + Instance Type
        * EC2 User Data
        * EBS Volumes
        * Security Groups
        * SSH Key Pair
    * Min Size/ Max Size/ Initial Capacity
    * Network + Subnets Information
    * Load Balancer Information - Target group information
    * Scaling Policies
* Auto Scaling Alarms
    * scale an ASG based on CloudWatch alarms
    * an Alarm monitors a metric (such as Average CPU)
    * metrics are computed for overall ASG instances
* Auto Scaling new rules
    * target average CPU usage
    * number of requests on the ELB per instance
    * average network in/out
* ASG Brain Dump
    * Scaling policies can be on CPU, Network, custom metrics, schedule (if you know your visitors pattern) 
    * ASGs use Launch Configurations or Launch Templates  
    * to update an ASg you must provide a new launch configuration/launch template
    * IAM roles attached to ASG will be assigned to EC2 instances
    * ASG are free, pay for the underlying resources being launched
    * if they get terminated for whatever reason, the ASG will automatically create new ones as a replacement. Extra safety. 
   
### ASG - Scaling policy ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19733728#overview
* TargetTracking Scaling
    * Most simple and easy to set up
    * Example1: I want to the average ASG CPU to stay at around 40% 
* Simple/Step Scaling
    * When a CloudWatch alarm is triggered (example CPU > 70%), then add 2 units
    * When a CloudWatch alarm is triggered (example CPU < 30%), then remove 1 unit
* Scheduled Actions
    * Example: increase the min capacity to 10 at 5 pm on Friday
    
### ASG - Scaling cooldowns ###
* period helps to ensure that your Auto Scaling group doesn't launch or terminate additional instances before the previous scaling activity takes effect
* in additional to default cooldown for Auto Scaling group, we can create cooldowns that apply to a specific simple scaling policy
* default is 300 seconds          
        
### Common security group setting ###
User -> ELB
    * Type: HTTP / HTTPS
    * Protocol: TCP / TCP
    * Port: 80 / 443
    * Source: 0.0.0.0/0 / 0.0.0.0/0
    
ELB -> EC2
    * Type: HTTP
    * Protocol: TCP
    * Port: 80
    * Source: sg-1231231... (id of security of LB, allow only load balancer ip)      
* Troubleshooting 
    * 4xx errors are client induced errors
    * 5xx errors are application induced errors
    * Load Balancer Errors 503 means at capacity or no registered target
    * if the LB can't connect, check security groups
* Monitor 
    * ELB access logs will log access requests (debug per request) 
    * CloudWatch Metrics will give you aggregate statistics (ex: connections counts) 
    
### Creating classic ELB - CLB ###
1.Go to "EC2" service
2.Find on left menu "Load Balancers"
3.Create load balancer colour button
4.Select "classic" ELB  
5.Use default settings 
6.Create new security group 
    * type: Custom
    * protocol: TCP
    * port: 80
    * source: 0.0.0.0/0
7.Set up health checks  
8.Launch instance  
9.Use DNS in "description" tab to check if CLB works properly  
10.Edit security groups "service EC2", allows only load balancer id as "source" 

### Creating application LB - CLB ###
1.Go to "EC2" service
2.Find on left menu "Load Balancers"
3.Create load balancer colour button
4.Select "Application Load Balancer" 
5.AZ - select all AZ's and next
6.Use security group from classic load balancer 
7.Configure routing
    * Name: 
    * Target type: instance 
    * protocol: TCP
    * port: 80
7.Register targets
    * select instance for target group

### Creating autoscaling group ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851246#overview
1.Go to "EC2" service  
2.Find on left menu "Auto Scaling/Auto Scaling Group"  
3."Create an Auto Scaling group"  
4."Create launch template"  
    * add name  
    * select AMI   
    * instance type  
    * network setting - VPC  
    * security groups
    * advance details/ User data  
    * "Create launch template"  
5.Back to Autoscaling group and select created launch templete  
6.Check setting and click next  
7.Select subnet
8.Specify load balancing  
    * Enable load balancing - select ALB  
    * select target group  
    * Health checks - EC2, ELB - checked  
9.Group size and scaling policies  
10.Notification - skip  
11.Tags - skip
12.Review and Create ASG

