### KMS - Request Quotas
* when you exceed a request quota, you get a Throttling Exception
* to response use **exponential backoff** (backoff and retry)
* for cryptographic operations, they share a quota
* this includes requests made by AWS on your behalf (ex.SSE-KMS) 
* for GenerateDataKey, consider using DEK caching from the Encryption SDK
* you can request a Request Quotas increase through API or AWS support
