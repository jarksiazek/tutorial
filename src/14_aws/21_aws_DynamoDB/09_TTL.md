### DynamoDB TTL (Time to Live)
* TTL = automatically delete an item after an expiry date/time
* TTL - is provided at no extra cost, deletions do not use WRC/RCU
* TTL is background task operated by the DynamoDB service itself
* helps reduce storage and manage the table size over time
* helps adhere to regulatory norms 
* TTL is enabled per row (you define a TTL column and add a date here)
* DynamoDB typically deletes expired items within 48 hours of expiration
* deleted items due to TTL are also deleted in GSI/LSI
* DynamoDB Streams can help recover expired items
* 
