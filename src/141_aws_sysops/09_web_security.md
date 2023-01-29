### DDOS
* AWS Shield Standard
* AWS Shield Advanced - premium 
* AWS WAF - filter specific requests based on rules
* cloudfront route53
* user -> Route53(Shield) -> cloudfront(shield, waf) -> vpc -> security groups -> elb(public) -> ec2(private)
* aws shield
  * standard
    * SYN/UDP Floods, Reflection attacks 
    * layer3/ layer 4 attacks
  * advanved
    * 3k per org
    * more protection against DDoS
    * 24/7 support   
* aws waf
  * layer 7
  *  deploy on ALB, API Gateway, Cloudfront
  *  define Web ACL 
  *  protect from SQL injection, Cross-site scriptiny XSS
  *  size contraints, geo-match 
  *  rate based rules (count accurrences of events) - DDos protection
### Amazon Inspector
* automated security assessments
* reports to AWS Security Hub and Eventbridge
* EC2
  * leveraring the SSM agent
  * Analyze against unintended network accessibilty
  * analyze running OS against known vulnerability
* ECR 
  * analyze containers against vulnerability
* Lambda
  * software and packages vulnerability
 * 
