# Map #
* dictionary
* key value pair
```python
customer  = {
    "name": "John",
    "age": 10,
    "is_verified": True
}

customer["name"] # "John"

customer["birthdate"] # Error
customer.get("birthdate") # None
# customer.get("birthdate, "Jan 1 1980") #birthdate does not exist use default value Jan 1 1980
```