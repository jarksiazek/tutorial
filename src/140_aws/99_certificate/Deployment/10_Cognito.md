### Q1
Data in Cognito needs to be further analyzed using Redshift. You planning to use Kinesis stream to the purpose.  
Which of the following can be performed to have Cognito Event push events to Kinesis stream to get analyzed data from Amazon Redshift? 
* Only use existing Kinesis Stream and create an IAM role which grants Amazon Cognito permission to this existing Stream
* **Use an existing Kinesis Stream o Create a new Kinesis Stream and create IAM role which grants Cognito permission to publish to Stream**
    * https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-streams.html
* Create a new kinesis stream instead of using Kinesis stream and create an IAM user with permission to Cognito to publish to this new stream
* Create a new Kinesis Stream an enable Cognito Stream which will automatically start putting events in the selected stream 