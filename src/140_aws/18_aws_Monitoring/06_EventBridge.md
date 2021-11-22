### AWS EventBridge
* Next evolution of CloudWatch Events
* Default event bus: generated by AWS services (CloudWatch Events)
* On EventBridge we can add additional event buses: 
    * Partner event bus: receive events from SaaS service or applications (Zendesk, DataDog, Segment, AuthO, ect)
    * Custom event bus: for your own applications
    * event buses can be accessed by other AWS accounts 
    * can create rules how to process the events (similar to CloudWatch events)

### AWS EventBridge Schema Registry
* EventBridge can analyze the events in your bus and infer the schema
* The schema Registry allows you to generate code for your application that will know in advance how data is structured in the event bus