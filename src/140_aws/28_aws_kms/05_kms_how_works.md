### API - Encrypt and Decrypt data < 4kb
![](images/aim5.jpg)
* Encrypt
    1. Sending plaintext to KMS using Encrypt API and specify CMK to use
    2. KMS checking IAM user permissions
    3. Perform encryption
* Decrypt
    1. Perform decryption (knows CMK - info in encrypted file)
    2. Check IAM permissions
    3. Sending decryped file
     
### Envelope encryption data > 4kb
* data more than bigger than 4kb
* anything over 4kb of data that needs to be encrypted must be use the Envelope Encryption == GenerateDataKey API
* Encrypt
![](images/aim6.jpg)
    1. Sending big file (10MB) to KMS using Encrypt API and specify CMK to use
    2. KMS generates DATA KEY 
    3. send back plaintext data key (plaintext DEK)
    4. client side encryption using DEK and creating **encrypted file + encrypted DEK**
* Decrypt
![](images/aim7.jpg)
    1. **encrypted file + encrypted DEK** - KMS encrypt only DEK file and send it to user
    2. client side encryption using encrypted file and decrypted DEK
    
### Encryption SDK
* the AWS Encryption SDK implemented Envelope Encryption for us
* the encryption SDK also exists as a CLI tool we can install
* implementation for Java, Python, C, JavaScript
* feature - data key caching
    * re-use data keys instead of creating new ones for each encryption
    * helps with reducing the number of calls to KMS with a security trade-off
    * use LocalCryptoMaterialsCache(max age, max bytes, max number of messages)
