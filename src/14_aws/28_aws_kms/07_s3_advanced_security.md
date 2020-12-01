### S3 Encryption for Objects
* there are 4 methods of encrypting objects in S3
    * SSE-S3: encrypts S3 objects using handled and managed by AWS
    * SSE-KMS: leverage AWS KMS to manage encryption keys
    * SSE-C: when you want to manage your onw encryption keys
    * Client Side Encryption
    
### SSE_KMS
* encryption using keys handled and managed by KMS
* KMS Advantages: user control + audit trail 
* object is encrypted server side
* must set header "x=amz-server-side-encryption":"aws:kms"

### SSE_KMS Deep Dive
* leverage **GenerateDataKey** and **Decrypt**
* these KMS API calls will show up in CloudTrail, helpful for logging
* to perform SSE-KMS:
    * a KMS Key Policy that authorizes the user/role
    * an IAM policy that authorizes access to KMS 
    * otherwise you will get an access denied error
* S3 calls to KMS for SSE=KMS count against your KMS limits 
    * if throttling -> exponential backoff
    * if throttling -> change limits

### Force SSE_KMS
* deny incorrect encryption header: make sure it includes aws:kms 
* deny no encryption header to ensure objects are not uploaded un-encrypted
*  
    
### Force SSL 
* to force SSL, create S3 bucket policy with a DENY on the condition **aws:SecureTransport=false**
* using an allow on **aws:SecureTransport=true** would allow anonymous GetObject if using SSL