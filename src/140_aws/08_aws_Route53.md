### Route53  ###
* Route53 is a Managed DNS (Domain Name System)
* DNS is a collection of rules and records which helps clients understand how to  reach a server through its domain name
* Global
* Most common records: 
    * A: hostname to IPv4
    * AAAA: hostname to IPv6
    * CNAME: hostname to hostname
    * Alias: hostname to AWS resource
 ![](.08_aws_Route53_images/aim1.jpg) 
* Route53 can use
    * public domain names you own (or buy)  
        example.mydomain.com
    * private domain names that can be resolved by your instances in your VPCs
        example.mydomain.internal
* Route53 advance features
    * Load balancing (though DNS - also called client load balancing)
    * Health checks (althrough limited...)
    * Routing policy: simple, failover, geolocation, latancy, weighted, multi value
* You pay $0.50 per month per hosted zone
* "nslookup" to verify if domain is assigned correctly 

### DNS Records TTL ###
* web browser remembers the ip address for some time 
* TTL can be customized
* TTL is mandatory for each DNS record

### CNAME vs Alias ###
* CNAME
    * Points a hostname to any other hostname (app.mydomain.com =>blabla.anything.com)
    * ONLY FOR NON ROOT DOMAIN (ex. something.mydomain.com)
* Alias
    * Points a hostname to an AWS Resource (app.mydomain.com =>blabla.amazon.com)
    * Works for ROOT DOMAIN and NON ROOT DOMAIN (ex. mydomain.com)
    * free of charge
    * native health check
    
### Routing policy ###
* Simple 
    * no health checks attached
    * if multi values are returned, a random one is chosen by the client
* Weighted 
    * controls that % of the request goes to specific endpoint
    * example: test scenario when 1% of traffic goes to new version of app 
    * health checks
* Latency
    * redirects to server that has the least latency close to us
    * useful when latency of users is a priority
    * Germany may be directed to the US (if that's the lowest latency)
* Failover
    * if primary ip is unhealthy all traffic will be sent to secondary ip
    * only one primary and one secondary should be set  
    * is associated with health checks
* Geo Location
    * Different from Latency based
    * based on user location Country, Continent 
    * traffic from the UK should go to this specific IP
    * should create a "default" policy (in case there's no match on location)
* Multi Value 
    * use when routing traffic to multiple resources
    * want to associate a Router 53 health checks with records
    * up to 8 healthy records are returned for each Multi Value query
    * Multi Value is not a substitute for having an ELB
     


### Health checks ###
* have x health checks failed => unhealthy (default 3)
* after x health checks passed => health (default 3)
* default Health Check Interval: 30s (can set to 10s - higher cost)
* about 15 health checkers will check the endpoint health
* HTTP, TCP, HTTPS (no SSL verification)
* possibility of integrating the health check with CloudWatch

    
    
    
    
### Create Domain - Route53  ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19728942#overview


