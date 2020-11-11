# Lambda BuiltInFunctions #

### Functional Interfaces
Interface | Method | Description | Common Use
--- | --- | --- | ---
Predicate<T> | boolean test(T t) | checks conditions | filter()
Consumer<T> | void accept(T t) | takes argument and return nothing | forEach()
Function<T,R> | R apply(T t) | takes argument and return result | map()
Supplier<T> | T get() | operations return value to caller | generate()

### Predicate
```java
import java.util.function.Predicate;
public class PredicateTest {
    public static void main(String []args) {
        Predicate<String> nullCheck = arg -> arg != null;
        Predicate<String> emptyCheck = arg -> arg.length() > 0;
        Predicate<String> nullAndEmptyCheck = nullCheck.and(emptyCheck);
        
        String helloStr = "hello";
        System.out.println(nullAndEmptyCheck.test(helloStr));
    
        String nullStr = null;
        System.out.println(nullAndEmptyCheck.test(nullStr));
    }
}
```

### Consumer
```java
Consumer<String> printUpperCase = str -> System.out.println(str.toUpperCase());
printUpperCase.accept("hello");
// prints: HELLO
```

### Function
```java
Function<String, Integer> strLength = str -> str.length();
System.out.println(strLength.apply("supercalifragilisticexpialidocious"));
// prints: 34

Function<Integer, Integer> negate = (i -> -i), square = (i -> i * i),
negateSquare = negate.compose(square);
System.out.println(negateSquare.apply(10));
//return -100 (10*10 -> -1)
```
* *andThen()* vs *compose()* 
    * *andThen()* - applies the passed argument after function
    * *compose()* - applies the passed argument before function
    
### Supplier
```java
Supplier<String> currentDateTime = () -> LocalDateTime.now().toString();
System.out.println(currentDateTime.get());
```
```java
Supplier<String> newString = () -> new String();
System.out.println(newString.get());

Function<String, Integer> anotherInteger = Integer::new;
System.out.println(anotherInteger.apply("100"));
// this code prints: 100
```

### BinaryOperators 
Similar to functional but takes 2 arguments
```java
BiFunction<String, String, String> concatStr = (x, y) -> x + y;
System.out.println(concatStr.apply("hello ", "world"));
// prints: hello world

BiFunction<Double, Double, Integer> compareDoubles = Double::compare;
System.out.println(compareDoubles.apply(10.0, 10.0));
// prints: 0
```