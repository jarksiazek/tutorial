### Nested Classes ###
* non-local
    * static 
    ```java
    class Outer {
      static class StaticNested {
      }   
    }
    ```
    * non-static
    ```java
    class Outer {
      class Inner {
      }   
    }
    ```
* local 
    * non-static
    ```java
    class Outer {
      void foo() {
          class LocalInner {
          }
      }   
    }
    ```
    * anonymous
        * anonymous
        ```java
        class Outer {
          void foo() {
              return new Object(){
                  public String toString(){
                      return "anonymous";
                  }      
              };       
          }   
        }
        ```
      
### Nested Classes - STATIC ###
* accessibility is defined by the outer class
* the name of static class is expressed with OuterClassName.NestedClassName
* static nested can be declared abstract or final
* static nested can extend another class or they can be used as base classes
* static nested class can have static members
* static nested classes cna access the members of the other class
* outer class can access members(even private members)

```java
class Outer { // an outer class has a static nested class
    static class Inner {}
}
interface Outer { // an outer interface has a static nested class
    static class Inner {}
}
class Outer { // an outer class has a static nested interface
    static interface Inner {}
}
interface Outer { // an outer interface has a static nested interface
    static interface Inner {}
}
```
Example 1 
```java
abstract class Shape {
    public static class Color {
        int m_red, m_green, m_blue;
    
        public Color(int red, int green, int blue) {
            m_red = red; m_green = green; m_blue = blue;
        }
        public String toString() {
            return " red = " + m_red + " green = " + m_green + " blue = " + m_blue;
        }
    }
}

public class TestColor {
    public static void main(String []args) {
    Shape.Color white = new Shape.Color(255, 255, 255);
    System.out.println("White color has values:" + white);
    }
}
// White color has: red = 255 green = 255 blue = 255
```

### Nested Classes - INNER CLASS ###
* accessibility is defined by outer class
* inner class can extend a class or can implement interfaces
* inner class can be final or abstract
 
```java
class Outer { // an outer class has a inner class
    class Inner {}
}
class Outer { // an outer class has a inner interface
    interface Inner {}
}
```
Example 1 
```java
public class Circle {
    class Point {
        int xPos, yPos;
    
        public Point(int x, int y) {
            xPos = x; yPos = y;
        }
        public String toString() {
            return "(" + xPos + "," + yPos + ")";
        }
    }
    
    private Point center; 
    private int radius; 

    public Circle (int x, int y, int z){
        center = this.new Point (x,y);
        radius = r;
    }

    public String toString() {
        return "mid point = " + center + " and radius = " + radius;
    }   
}

public class TestColor {
    public static void main(String []args) {
    Circle circle = new Circle(255, 255, 255);
    System.out.println(circle);
    }
}
// mid point = (255,255) and radius = 255;
```

### Local Inner Classes ###
* you can pass only final variables to local inner class
* can create a non-static local class inside as body of code 
* local classes are accessible only from the body of the code 
* can extend a class or implement interface while defining a local class
* local class can access all the variables available in the body 
```java
class someClass { 
    void someFunction(){
        class Local{}
    }
}
```
Example 1 
```java
abstract class Shape {
    public static class Color {
        int m_red, m_green, m_blue;
        public Color() {
            this(0, 0, 0);
        }
        public Color(int red, int green, int blue) {
            m_red = red; m_green = green; m_blue = blue;
        }
        public String toString() {
            return " red = " + m_red + " green = " + m_green + " blue = " + m_blue;

        }
    }
}
class StatusReporter {
    // important to note that the argument "color" is declared final
    static Shape.Color getDescriptiveColor(final Shape.Color color) {
        // local class DescriptiveColor that extends Shape.Color class
        class DescriptiveColor extends Shape.Color {
            public String toString() {
                return "You selected a color with RGB values" + color;
            }
        }
    return new DescriptiveColor();
    }
    public static void main(String []args) {
        Shape.Color descriptiveColor = StatusReporter.getDescriptiveColor(new Shape.Color(0, 0, 0));
        System.out.println(descriptiveColor);
    }
}
```

### Anonymous Inner Classes ###
* anonymous classes are defined in the new expression itself
* you cannot explicitly extend a class or explicitly implement interface when defining an anonymous class 
```java
class someClass { 
    void someFunction(){
        new Object(){};
    }
}
```

```java
class StatusReporter {
    static Shape.Color getDescriptiveColor(final Shape.Color color) {
        return new Shape.Color() {
            public String toString() {
                return "You selected a color with RGB values" + color;
            }
        };
    }
    public static void main(String []args) {
        Shape.Color descriptiveColor = StatusReporter.getDescriptiveColor(new Shape.Color(0, 0, 0));
        System.out.println(descriptiveColor);
    }
}
```