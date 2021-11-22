### API Gateway - HTTP API vs REST API
* HTTP 
    * low-latency, cost-effective AWS Lambda proxy
    * HTTP proxy APIs and private integration(no data mapping)
    * support OIDC and Oauth 2.0 authorization, and built-in support for CORS
    * no usage plans and API keys
* REST
    * All features (except Native OpenID Connect/ OAuth 2.0)

### API Gateway - WebSocket
* WebSocket 
    * 2 ways interactive communication between a user's browser and a server
    * server can push information to the client
    * this enables stateful application  use cases
* WebSocket APIs are often used in real-time applications such as 
    * chat applications 
    * collaboration platforms
    * multiplayer games
    * financial trading platforms
* Works with AWS Services
 
