### Integration Types ###
* **MOCK**
    * API Gateway return a response without sending the request to the backend

* **HTTP/AWS (Lambda & AWS Services)**
    * you must configure both the integration request and integration response
    * setup data mapping using **mapping templates** for the request and response
    ![](images/aim2.jpg)

* **AWS_PROXY (Lambda Proxy)**
    * incoming request from the client is the input to Lambda
    * the function is responsible for the logic of request/response
    * No mapping templates
    * headers, query string parameters are passed as arguments
    ![](images/aim3.jpg)

* **HTTP_PROXY**
    * no mapping templates
    * the HTTP request is passed to the backend
    * the response form backend is forwarded by API Gateway
    ![](images/aim4.jpg)
    
### Mapping Templates (AWS & HTTP Integration) ###
* mapping templates can be used to modify request/responses
* rename/modify query string parameters
* modify body content
* add headers
* uses **Velocity Template Language(VTL)**: for loop, if etc...
* filter output results (remove unnecessary data)

### Mapping Example: JSON to XML with SOAP ###
![](images/aim5.jpg)
* SOAP API are XML based, whereas REST API are JSON based
* API Gateway should
    * extract data from the request: either path, payload or header
    * build SOAP message based on request data (mapping template)
    * call SOAP service and receive XML response
    * transform XML response to desired format (like JSON) and response to the user

### Mapping Example: Query String parameters
![](images/aim6.jpg)    
