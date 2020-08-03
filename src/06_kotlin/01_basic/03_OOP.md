### classes
1) New -> Kotlin class/file
2) Name class

* example 1
```kotlin
class Person(firstName: String, lastName: String) {
    init {
        print("Create a person with $firstName and $lastName")    
    }
}

val me = Person("John", "Smith")
```

* example 2 with constructor uses for annotation or modifier 
```kotlin
class Person constructor(firstName: String, lastName: String) {
    
}
```

* example 3 with modifier 
```kotlin
class Person internal constructor(firstName: String, lastName: String) {
    init {
        print("Create a person with $firstName and $lastName")    
    }
    
    //secondary constructor
    constructor(firstName: String, lastName: String, age: Int) : 
        this(firstName, lastName) {
        
    }
}
```

### object
* example 1 
```kotlin
   val  location = object { 
    var xPosition = 200            
    var yPosition = 100     
    fun printLocation() {
        println("Position = (${xPosition, yPosition})")
    }   
}
println("Position = (${location.xPosition, location.yPosition})")

location.printLocation()
```

### interface
* example 1 
```kotlin
interface Vehicle {
    val makeName: String
    fun go() {
        println("Vroom, vroom")
    }

    fun getDoors(): Int
}

class Car: Vehicle {
    override val makeName = "Ford"
    override fun getDoors(): Int {
        return 5  
    }
}
```

### generics
* example 1 
```kotlin

fun <T: Comparable<T>> max(param1: T, param2: T): T {
    val results = param1.compareTo(param2)
    return if(results > 0) param1 else param2
} 

val maxInt: Int = max(42, 99)
val maxLong: Long = max(123L, 99L)
```
