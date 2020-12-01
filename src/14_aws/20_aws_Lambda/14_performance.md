### Lambda performance ###
* RAM
    * from 128 to 3008 MB in 64 increments
    * the more RAM you add, the more vCPU credits you get
    * at 1792 MB, a function has the equivalent of one full vCPU
    * after 1792 MB, you get more than one CPU, and need to use multi-threading in your code to benefit form it
* Timeout
    * default 3 sec, max is 900 seconds (15 mins)

### Lambda execution context ###
* is temporary runtime environment that initializes any external dependencies of your lambda code
* great for database connections, HTTP clients, SDK clients
* the execution context is maintained for some time in anticipation of another Lambda function invocation
* the next function invocation can "re-use" the context to execution time and save time in initializing connections objects
* the execution context includes the /temp directory

Db connection is established once and re-used across invocations
```python
import os

DB_URL = os.getenv("DB_URL")
db_client = db.connect(DB_URL)

def get_user_handler(event, context):
    user = db_client.get(user_id = event["user_id"])
    return user
```     

### Lambda /tmp space ###
* if Lambda needs to download the big file to work 
* if Lambda needs disk space to perform operations
* you can use /tmp directory with max size 512 MB
* the directory content remains when the execution context is frozen, providing transient cache that can be used for multiple invocations (helpful to checkpoint your work)
* for permanent persistence of object (non temporary), use S3
* 