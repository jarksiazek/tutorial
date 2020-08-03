# Functions #
### void  ###
```python
def function_name(name):
    print(f'Hi {name}')
    print("This also part of the function") 
# 2 lines breaks between function definition and the rest of the code

function_name("John")
```

```python
def function_name(first_name, last_name):
    print(f'Hi {first_name} {last_name}')
    print("This also part of the function") 
# 2 lines breaks between function definition and the rest of the code

#position argument
function_name(last_name="Smith", first_name="John")
```

### return  ###
```python
def square(number):
    res = number * number
    return res

res = square(3)

```