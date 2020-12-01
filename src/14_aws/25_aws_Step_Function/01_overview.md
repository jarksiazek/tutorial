### Overview ###
* build serverless visual workflow to orchestrate Lambda functions
* represent flow as a JSON state machine
* features: sequence, parallel, conditions, timeouts, error handling
* can also integrate with EC2, ECS, on premise server, API Gateway
* max execution time is 1 yr
* possibility to implement human approval feature
* use cases:
    * order fulfillment
    * data processing
    * web applications
    * any workflow

### Error handling ###
* any state can encounter runtime errors for various reasons
    * state machine definition issues (eg. no matching rule in a Choice state)
    * task failure (eg. an exception in Lambda)
    * transient issue (eg. network partition events)
* by default, AWS Step Functions causes the execution to fail entirely
* option to handle a failure
    * option 1 - retry failures - Retry: IntervalSeconds, MaxAttempts, BackoffRate
    * option 2 - move on - Catch: ErrorEquals, Next
* best practice is to include data in the error messages

 ### Step Function Standard vs Express ###
 Feature | Standard |  Express 
 --- | --- | --- 
 Max duration | 1 yr | 5 minutes
 Supported execution start rate | over 200 per second | over 100000 per sec
 Supported state transition rate | over 4000 per sec per account | Nearly unlimited
 Pricing | priced per state transition(more expensive) | priced per execution(cheaper) 
 Execution history | visually debugged, cloudwatch logs | CloudWatch logs
 Execution semantics | exactly-one workflow execution | at-least once workflow execution 
