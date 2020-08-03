# Exceptions #
```python
try: 
    age = int(input('Age '))
    print(age)
except ZeroDivisionError:
    print("Age cannot be 0")
except ValueError: #reacts on ValueError type of exception
    print("Invalid value")
```