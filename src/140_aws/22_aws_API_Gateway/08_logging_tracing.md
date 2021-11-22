### API Gateway - Logging and tracing
* CloudWatch Logs
    * enable CloudWatch logging at the Stage level (with log level)
    * can override settings on a per API basis (ex.ERROR,DEBUG,INFO)
    * log contains information about request/response
*X-Ray
    * enable tracing to get extra information about requests in API Gateway
    * X-Ray API Gateway + AWS Lambda gives you full picture
   
### API Gateway - Metrics
* metrics are by stage, possibility to enable detailed metrics
* **CacheHitCount** & **CacheMissCount** efficiency of the cache
* **Count** the total number of API requests in a given period
* **IntegrationLatency** time between when API Gateway relays a request to the backend and when it receives a response from the backend
* **Latency** time between API Gateway receives a request from a client and when it returns a response to the client. The latency includes the integration latency and other API Gateway overhead.
* **4XXError** (client-side) & **5XXError** (server-side)

### API Gateway throttling
*  **Account Limit**
    * API Gateway throttles requests at 10000 rps across all API
    * Soft limit that can be increased upon request
* in case of throttling => 429 **TooManyRequests**
* can set stage limit and method limits to improve performance
* or you can define Usage Plans to throttle per customer

### API Gateway errors
* 4xx - client errors
    * 400 Bad Request
    * 403 Access Denied, WAF filtered
    * 429 Quota exceeded, Throttle
* 5xx - server errors
    * 502 - Bad Gateway Exception, usually for an incompatible return from a Lambda proxy integration backend or for out-of-order invocations due to heavy load
    * 503 - service unavailable exception
    * 504 - integration failure - ex Endpoint Request Timeout
    
 