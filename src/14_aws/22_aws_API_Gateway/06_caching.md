### Caching API responses ###
* reducing number of calls made to the backend
* default TTL cache is 300 seconds (min 0, max 3600s)
* one cache per stage
* possible to override cache settings per method
* cache encryption option
* cache size 0.5GB - 237GB
* cache is expensive, makes sense in production, may not make send in dev/test
 
### Caching Invalidation ###
* able to flush the entire cache
* clients can invalidate the cache (with proper IAM authorization) with **header: Cache-Control:max-age=0**
* if you don't impose an InvalidateCache policy (or choose the Require authorization check box in console), any client can invalidate the API cache
* 