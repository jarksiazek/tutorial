### CloudFront ###
* Content Delivery Network (CDN)
* improves read performance, content is cached at the edge
* 216 points of edge locations globally      
* DDoS protection, integration with Shield, AWS Web Application, Firewall
* can expose external HTTPS and talk to internal HTTPS backends
![](.13_aws_CloudFront_images/aim1.jpg)

### CloudFront - Origins ###
* S3 bucket
    ![](.13_aws_CloudFront_images/aim2.jpg)
    * For distibuting files and caching them at the edge
    * Enhanced security with CloudFront Origin Access Identity (OAI)
    * can be used as an ingress (to upload files to S3)
* Custom Origin
    ![](.13_aws_CloudFront_images/aim3.jpg)
    * APL
    * EC2
    * S3 Website
    * Any HTTP backend you want
    
### CloudFront -  Geo Restriction ###
* restrict who can access your distribution
    * whitelist: allow your users to access your content only if they are in one of the countries on a list of approved countries
    * blacklist: do not allow user from these countries
     
### CloudFront - S3 Cross Region Replication ###
* CloudFront
    * Global Edge Network
    * Files are cached for a TTL
    * Great for static content that must be available everywhere

* S3 Cross Region Replication
    * Must be setup for each region you want replication to happen 
    * files are updated in near real-time
    * read only
    * great for dynamic content that needs to be available at low-latency in few regions

### CloudFront - S3 Caching ###
* Cache based on 
    * Headers
    * Session Cookie
    * Query String Parameters
* The cache lives at each CloudFront Edge Location
* You want to maximize the cache hit rate to minimize requests on the origin
* Control the TTL (0 sec to 1 year), can be set by the origin using Cache-Control header, Expires header
* You can invalidate part of the cache using the CreateInvalidation API

### CloudFront - Security ###
* Geo Restriction 
    * whitelist - allowing access from selected countries
    * blacklist - restricting access from selected countries
* HTTPS
    * Viewer Protocol Policy
        * Redirect HTTP to HTTPS
        * use only HTTPS
    * Origin Protocol Policy (HTTP or S3)
        * HTTPS only
        * Match Viewer
          (HTTP => HTTPS & HTTPS => HTTPS)                
          
### CloudFront - Signed URL/Signed Cookies ###
![](.13_aws_CloudFront_images/aim4.jpg)
* You want to distribute paid shared content to premium users over the world
* We can use CloudFront Signed URL /Cookie. We attach a policy with
    * URL expiration
    * IP ranges to access the data from 
    * trusted signers (which AWS accounts can create signed URLs)
* How long should the URL be valid for? 
    * Shared content (movie, music): make it short (a few minutes)
    * Private content (private to the user): you can make it last for years 
* Signed URL vs Cookie
    * Signed URL - access to individual file (one signed URL per file)
    * Signed Cookies - access to multi files (one assigned cookie for many files)
* CloudFront Signed URL vs S3 Pre-Signed URL
    * CloudFront Signed URL
        * allow access to a path, no matter the origin
        * account wide key-pair, only the root can manage it
        * can filter by IP, path date, expiration
        * can leverage caching features
    * S3 Pre-Signed URL
        * Issue a request as the person who pre-signed URL
        * uses the IAM key of the signing IAM principal 
        * Limited lifetime

            
   