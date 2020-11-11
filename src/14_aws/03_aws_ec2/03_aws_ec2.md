### EC2 ###
https://aws.amazon.com/ec2/instance-types/
https://www.ec2instances.info/
* virtual machine - EC2
* storing data on virtual drivers - EBS
* distributing load across machines - ELB
* scaling the services using an auto-scaling group - ASG
* by default, private IP for internal AWS Network
* by default, public IP for the WWW
* stop and start, changing public ip
* characteristics
    * RAM (type, amount, generation)
    * CPU (type, make, frequency, generation, cores)
    * I/O (disk performance, EBS optimisations)
    * Network (network bandwidth, network latency)
    * GPU - Graphical Processing Unit
* M instance types are balanced - Good RAM, CPU, I/O, Network, No CPU
* T2/T3 instance types are "burstable"
    * T2 
        * Overall good performance, when the machine needs to process something unexpected, it can burst and CPU can be VERY good 
        * Burst unexpected load, it is limited ("burst credits")
        * when low on credit, you need to move to a different kind of non-burstable instance
        * T2 Unlimited - unlimited burst credit balance

### EC2 instance types ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/13863792#overview
* <strong>On Demand Instances:</strong> short workload, predictable pricing
    * pay for what you use (billing per sec, after first minute)
    * the highest cost per second
    * no long term commitment
* <strong>Reserved:</strong> minimum 1 year
    * Reserved Instances: long workloads
        * up to 75% discount compared to "On demand"
        * pay upfront 
        * reservation 1 or 3 yrs
        * specific instance type
        * perfect for database
    * Convertible Reserved Instances: long workloads with flexible instances (small today, big tomorrow)
        * up to 54% discount compared to "On demand"
        * can change the EC2 instance type
        * more expensive than "reserved instances", more flexible
    * Scheduled Reserved Instances: example every Thursday 3am to 6am
        * launch on time window e.g. everyday 3am to 6 am 
        * require a fraction day/week/month
        * up to 10% discount compared to "On demand" 
* <strong>Spot Instances:</strong> short workload, for cheap, can lose instance
    * up to 90% discount compared to "On demand" 
    * instance that you can lose ath the point of time if your max price is less than the current spot price
    * the most cost-efficient instance in AWS
    * useful for workload that are resilient to failure
        * Batch jobs
        * Data analysis
        * Image processing, etc
    * Not for critical jobs or databases
* <strong>Decimated Instances:</strong> no other customers will share hardware
    * Instances running on hardware that's dedicated to you
    * May share hardware with other instances in same account
    * No control over instance placement (can move hardware after Stop/Start)
* <strong>Decimated Hosts:</strong> book an entire physical server, control instance placement
    * physical dedicated EC2 server for your use
    * full control of EC2 Instance placement
    * visibility into the underlying sockets/ physical cores of the hardware
    * allocated for your account for a 3 year period reservation
    * more expensive
    * useful for software that have complicated licencing model (BYOL-Bring Your Own License)
    * useful for companies that have strong regulatory or compliance needs

### EC2 PRICING ###
https://aws.amazon.com/ec2/pricing/on-demand/
* cost per hour 
* varies base on 
    * Region
    * instance type
    * on-demand, spot, reserved, dedicated host 
    * operating system linux/Windows
* you are billed by the second with minimum of 60 seconds
* you are billed for storage, data transfer, fixed public IP, load balancing
* not pay when instance is stopped

### ENI Elastic Network Interface ###
* more info - https://aws.amazon.com/blogs/aws/new-elastic-network-interfaces-in-the-virtual-private-cloud/
* logical component in a VPC that represents a virtual network card
* EC2 access to the network
* Eth0 cannot be detached 
* Eth1 can be detached or move to other instance   
* ENI can have the following attributes: 
    * primary private IPv4 (Eth0) one or more secondary IPv4 (Eth1)
    * one Elastic IP (IPv4) per IPv4
    * one public IP IPv4   
    * one or more security groups
    * a MAC address - unique address manufacture network card
    * you can create ENI independently
    * attach on the fly, move to EC2 running instance
    * bound to specific AZ   
     
### START EC2 ###
1. AWS service - type EC2
2. Find and click color button - "Launch Instance"
3. Step1 - Select "Amazon Linux 2 AMI (HVM), SSD Volume Type" - training/free
4. Step2 - Select an Instance Type "t2.micro" - training/free 
5. Click "Review and Launch", the instance will be created or "Configure Instance Details"
6. Click "Configure Instance Details"
    * configure instance 
    * configure storage 
    * tags - marking instance (key/value)
    * security group 
        * create new security group 
        * Source in the table - Custom 0.0.0.0/0 - any ip
    * review and click launch
        * create or use existing key pair - access by SSH 

### ACCESS TO EC2 WINDOW 10 ###
1. Go to instance view and find "IPv4 Public IP" and copy that value
2. Open terminal and type, ip from "IPv4 Public IP" 
```bash 
$ ssh -i filePemDuringInstanceCreation.pem ec2-user@3.250.221.182
```
3. Verify user name  
```bash 
$ whoami
ec2-user
```
4. exit
```bash 
$ exit or ctrl + D
```

### INSTALL APACHE 2 ON EC2 ###
1.Connect to EC2 using cmd  
2.Switch to root 
```bash 
$ sudo us
```
3.Update machine
```bash 
$ yum update -y 
```
3.Install server
```bash 
$ yum install -y httpd.x86_64 
```
4.Start server 
```bash 
$ systemctl start httpd.service 
```
5.Enable start server after reboot 
```bash 
$ systemctl enable httpd.service 
```
6.See starting page
```bash 
$ curl localhost:80
```
7.To see page from point 7 on web, 
 * add security group which allows public connection on port 80 
 * open on a browser http:/publicId e.g. http://3.250.221.182/ 
 
8.To change default server page to "Hello world" 
```bash 
$ echo "Hello world" > /var/www/html/index.html
$ echo "Hello world from $(hostname -f)" > /var/www/html/index.html
```

### EC2 USER DATA ###
* bootstrap our instance using EC2 User data script
* runs during instance starts first time, only one
* Installing updates, installing software, download common files, etc
* Use "sudo" prefix

1.Create new instance EC2 
2.On "Configure instance" go down to "Advanced Details" 
3.Add script to install http server on "User data"
```text
#!/bin/bash
yum update -y 
yum install -y httpd.x86_64 
systemctl start httpd.service 
systemctl enable httpd.service 
echo "Hello world from $(hostname -f)" > /var/www/html/index.html
```
4.Add security group, allows SHH and HTTP  
5.Use existing pem or create new one  
6.Launch instances

### CUSTOM AMI OF EC2 ###
* reuse image of the instance
* AMI are built for a specific AWS region