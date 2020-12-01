### Messaging ###
* share information between services
* 2 patterns 
    * synchronous 
        * can be problematic if there are sudden spikes of traffic 
        * in that case is it better to **decouple** your application
            * using SQS - queue model
            * using SNS - pub/sub model
            * using Kinesis - real-time steaming model
    * asynchronous/ event based - middleware (queue)