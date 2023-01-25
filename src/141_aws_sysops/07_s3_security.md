### Encryption
* Server side Encryption - SSE
  * SSE-S3 enabled by default
    * managed by AWS
    * server-side
    * AES-256
    * header "x-amz-server-side-encyrption":"AES256" 
  * SSE-KMS - encryption using AWS KMS
    * user control + audit CloudTrail 
    * header "x-amz-server-side-encyrption":"aws:kms" 
  * SSE-C - customer-provided keys
    * not supported by console, only SDK or CLI
    * key managed outside of AWS
    * sending key to AWS
    * encryption key must provided in HTTP headers for every HTTP request made 
* Client Side Encryption
  * using Amazon S3 Client-side Encryption Library        
  * clients must encrypt data themselves before sending to S3

* In transit
  * SSL/TLS
  * HTTPS is mandatory for SSE-C   

### CORS
* Cross-Origin Resource Sharing 
* Origin = protocol(scheme) + host(domain) + port
* web browser based machanism to allow requests to other origins while visiting the main origin
* CORS Header - Access-Control-Allo-Origin

### Clacier Vault Lock
* Adopt a WORM (Write Once Read Many) model 
* create vault policy and lock policy

### S3 Object Lock
* blocking specific object for deleting
* versioning enabled
* WORM model
* Retention mode - Compliance:
  * object cannot be overwritten or deleted
  * retention mode and period can't be changed  
* Retention mode - Governance:
  * some users with special permissions can change rentetion or delete object

### S3 Access points
* access point - give access specific group to specific folder
