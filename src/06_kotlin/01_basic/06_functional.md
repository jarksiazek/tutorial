### lambdas
```kotlin
data class Student(val name: String, var age: Int)

fun getStudents(): List<Student> {
    return listOf(
        Student("Mark", 19), 
        Student("John", 29) 
    )
}

fun main(args: Array<String>) {
    val students = getStudents()
    val combos = students.map{ a -> a.name + ":" + a.age}

    val studentsWithLongName = students.filter{ it.name.length > 5}
    
    println("Comos: " + combos)
}
```
