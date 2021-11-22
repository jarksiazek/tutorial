# Class #
### built-in classes ### 
* Numbers
* Strings 
* Booleans
* Lists
* Dictionaries

### custom class ### 
```python
class Point: #Naming pattern similar to JAVA 
    #constructor, adding 2 extra fields x, y
    def __init__(self,x,y):
        sefl.x = x
        sefl.y = y 

    def move(self):
        print(f"move {self.x}")

    def draw(self):
            print("draw")    

# Creating object Point
point1 = Point()
point1.x = 10
print(point1.x)
point1.draw()
```