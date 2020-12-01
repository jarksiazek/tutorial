### KMS - Key Management Service
* anytime you hear "encryption" for an AWS service, it's most likely KMS
* easy way to control access to your data, AWS manages keys for us 
* fully integrated with IAM for authorization
* seamlessly integrated into
    * EBS - encrypt volumes
    * S3 - server side encryption of objects 
    * Redshift - encryption of data  
    * RDS - encryption of data  
    * SSM - parameter store
* but you can also use the CLI/SDK

### KMS - Customer Master Key (CMK) Types
* symmetric (AES-256 keys)
    * first offering of KMS, single encryption key that is used to Encrypt and Decrypt
    * AWS services that are integrated with KMS use symmetric CMKs
    * necessary for envelope encryption
    * you never get access to the key unencrypted (must call KSM API to use)

* asymmetric (RSA & ECC key pairs)
    * public (encrypt) and private key (decrypt) pair     
    * used for encrypt/decrypt or sign/verify operations
    * the public key is downloadable, but you access the Private Key unencrypted
    * use case: encryption outside of AWS by users who can't call the KMS API

### KMS - Details
* able to fully manage the key and policies
    * create 
    * rotation policies
* able to audit key usage (using CloudTrail)
* three types of customer master keys (CMK)
    * AWS Managed Service Default CMK:free
    * user Keys created in KMS: 1$/month
    * user Keys imported (must be 256-bit symmetric key): 1$/month
* pay for API call to KMS (0.03/10000 calls)

### KMS - When use?
* sensitive information
    * database password
    * credential to external service
    * private key of ssl certificates
* the value in KMS is that the CMK used to encrypt data can never be retrieved by user and the CMK can be rotated for extra security
* encrypted secrets can be stored in the code/ environment variables
* KMS can only help in encrypting up to 4 kb of data per call
* if data >4kb, use envelope encryption

### KMS - give access to someone
* make sure the Key Policy allows the user 
* make sure the IAM Policy allows the API calls

### Copying Snapshot across regions 
![](images/aim4.jpg)
* encrypted snapshot needs to have new KMS key in new region

### Copying Snapshot across accounts 
1. create snapshot, encrypted with own CMK
2. attach a KMS Key Policy to authorize cross-account access
3. share the encrypted snapshot
4. (in target) create a copy of the Snapshot, encrypt it with a KMS Key in your account 
5. create a volume from the snapshot

### KMS Key Policies
* control access to KSM keys, "similar" to S3 bucket policies
* difference: you cannot control access without them 
* default KSM Key Policy
    * created if you don't provide a specific KSM Key Policy
    * complete access to the key to the root user = entire AWS account
    * gives access to the IAM policies to the KSM key
* custom KSM Key Policy
    * define users, roles that can access the KSM key
    * define who can administer the key
    * useful for cross-account access of your KMS key


### KMS Summary
* **Encrypt** - up to 4 kb using KMS
* **GenerateDataKey** - unique symmetric data key (DEK)
    * returns a plaintext copy of the data key
    * a copy that in encrypted under the CMK that you specify
* **GenerateDataWithoutPlaintext** 
    * generate a DEK to sue at some point (not immediately)
    * DEK that is encrypted under the CMK that you specify (must use Decrypt later)
* **Decrypt**
    * upt to 4 kb (including Data Encryption Keys)     
* **GenerateRandom**
    * Return a random byte string
