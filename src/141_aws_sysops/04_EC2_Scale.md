### Load balancer
* Types
  * Classic Load Balancer
  * Application Load Balancer
    * HTTP, HTTPS, Websocket
  * Network Load balancer
    * TCP, TLS(secure TCP), UDP
  * Gateway Load Balancer
    * oparates at 3rd layer (Network layer) - Ip Protocol

### ALB - Application Load Balancer
* layer 7 (http)
* traffic: 
  * ALB -> target group 
  * ALB -> containers
* supports HTTP/2 and websocket
* Target groups
  * EC2, ECS tasks, lambda, ip addresses

### NLB - Network Load Balancer
* layer 4 - TCP, UDP 
* one static IP per AZ
* Target groups:
  * EC2, IP addresses (private)
  * Application Load Balancer 
  * Heath checks - TCP, HTTP, HTTPS 

### GWLB - Gateway Load Balancer
* layer 3 - ip packets
* uses the GENEVE protocol on port 6081
* deploy, scale, manage a fleet of 3rd party network virtual appliances in AWS
* eg. firewalls, intrusion detection and prenetion systems, deep packet inspection systems
* target groups
  * ec2, ip adressess (private) 

### SSL/TLS Certificates
* user to load balancer - in-flight encryption (in transit)
* SSL - Secure Socket Layer 
* TLS - Transport Layer Security (new SSL, mainly used)
* Public SSL - are issued by Certificate Authorities (CA)
* SSL have experiation date 
* Load Balancer usus X.509 certicate (SSL/TLS server certificate)
* Can be managed by ACM (AWS Certificate Manager)

### SNI - Server Name Indication
* solves the problem of loading multiple SSL certificaes onto one web server 

### Load Balancer Troubleshooting
* all metrics are pushed to CloudWatch metrics
 * Http codes
 * Latencty
 * RequestCount
 * RequestCountPerTarget
 * SurgeQueueLength - total requests that are pending routing yo a healthy instance. Helps to scale, max 1024
 * SpilloverCount (nadmiar) - total number of requests that were rejected because the surge queue is full
* logs 
 * can be stored in S3 (time, client ip, latencies, request paths, response, trace id 

### Target Groups Attributes
* deregistration delay - draining time
* slow start - warm-up time
* load balancing algorithm
 * Least Outstanding Requests - taking the instance with lower number of pending/unfinished requests
 * Round Robin - equally choose the targets  
 * Flow Hash - each tcp/udp connection is routed to a single target based on generated hash code
* stickness options

### Autoscaling Group
* scale based on CloudWatch alarms (eg CPU or any custom metric)
* target polices:
 * target tracking scaling
  * eg. average the ASG CPU to stay at 40 % 
 * simple/ step scaling
  * cloudwatch alarm (eg CPU > 70% then 2 units)    
 * scheduled actions
  * eg. Mon-Sun 2 units
 * predictive scaling
  * forcast load and schedule scaling ahead
* good metrics:
 * CPUUtilization, RequestCountPerTarget, Average Network In/Out, 

### Lifecycle hooks
* ASG - you can add custom hooks eg. after "pending" -> "pending:wait"

### ASG Metrics
* every 1 min
* ASG-level metrics:
 * GroupMinSize, GroupMaxSize, GroupDesiredSize
 * GroupServiceInstances, GroupPendingInstances, GroupStandbyInstances
 * GroupTerminatingInstances, GroupTotalInstances
* EC2-level
 * basic every 5 mins
 * detailed every 1 mins 
