### Q1
A developer is using API Gateway as an HTTP proxy to a backend endpoint. There are three separate environments.  
How should traffic be directed to different backend endpoints for each of these stages without creating a separate API for each? 
* Add a model to the API and add a schema to differentiate different backend endpoints
* **use stage variables and configure the stage variables in the HTTP integration Request of the API**
    * https://docs.aws.amazon.com/apigateway/latest/developerguide/stage-variables.html
    * stage variables are name-value pairs that you can define as configuration attributes associated with a deployment stage of an API.
* Use API Custom Authorizers to create an authorizer for each of the different stages
* Update the Integration Response of the API to add different backend endpoints

### Q2
You are a developer that has recently been hired for API expertise. The company is currently using API Gateway services for development.   
You need to control the behaviour of an API's frontend interactions. Which ogf the following could be done to achieve this? (select 2)  
* **Modify the configuration of the Method request**
    * control frontend interactions
* Modify the configuration of the Integration request
    * control backend interactions
* **Modify the configuration of the Method response**
* Modify the configuration of the Integration response

