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
* 
