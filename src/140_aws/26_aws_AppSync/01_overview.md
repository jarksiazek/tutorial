### Overview ###
![](images/aim2.jpg)
* AppSync is a managed service that uses **GraphQL**
    * **GraphQL** makes it easy for applications to get exactly the data they need
        ![](images/aim1.jpg)
        * this includes combining data from one or more sources
            * NoSQl data stores, Relational databases, HTTP APIs...
            * integrates with DynamoDB, Aurora, Elasticsearch and others
            * custom sources with AWS Lambda
* retrieve data in **real-time with WebSocket or MQTT on WebSocket**
* for mobile apps: local data access and data synchronization
* it all starts with uploading one **GraphQL schema**

### Security ###
* four ways you can authorize applications to interact with AWS AppSync GraphQL API
    * **API_KEY**
    * **AWS_IAM**: IAM users/ roles/ cross-account access
    * **OPENID_CONNECT**: OpenID Connect provider/ JWT
    * **AMAZON_COGNITO_USER_POOLS**   
 * for custom domain and HTTPS, use CloudFront in front of AppSync
 