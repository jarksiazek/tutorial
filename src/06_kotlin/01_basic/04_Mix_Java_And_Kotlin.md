### Java in Kotlin
```java
public class Animal {
    private final String name;
    private String kind;
    
    public String getName(){
        return name;
    }
    
    public void setName(String name){
        this.name = name;
    }

}
```

```kotlin
fun JavaInterop() {
    val Frisky = Animal()
     
    Frisky.name = "newName" //error
    Frisky.kind = "puma" //ok

    println(Frisky.toString())



    // 1. You can modify private fields without getters
    // 2. You can not modify private final fields

}
```

### Kotlin in Java
```kotlin
class Person internal constructor(var firstName: String, lastName: String) {
    init {
        println("Create..")
    }
    
    constructor(firstName: String, lastName:String, middleName: String): 
        this(firstName, lastName) {
        
    } 
}
```
```java
public class HelloWorld {
    public static void main(String[] args){
      Person person = new Person("Bob", "Miles");

      System.out.println("The person name is " + person.getFirstName());
    }
}
```