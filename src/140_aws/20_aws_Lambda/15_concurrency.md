### Lambda concurrency ###
* concurrency limit: up to 1000 concurrent executions
* concurrency limit by user - set a  **reserved concurrency** at the function level(=limit)
* each invocation over the concurrency limit will trigger a "Throttle"
* Throttle behaviour:
    * if synchronous invocation -> return ThrottleError - 429
    * if asynchronous invocation -> retry automatically and then to DLQ
* if you need a higher limit, open a support ticket

### Cold start and provisioned concurrency ###      
* cold start
    * new instance -> code is loaded and code outside the handler run (init)
    * this process can be time-consuming  
    * first request served by new instances has higher latency than the rest
* provisioned concurrency
    * concurrency is allocated before the function is invoked (in advance)
    * cold start never happens and all invocation have low latency
    * application auto scaling can manage concurrency (schedule or target utilization)
    *  