# Generics #
* 

### Generic class
```java
// This program shows container implementation using generics
class BoxPrinter<T> {
    private T val;
    public BoxPrinter(T arg) {
        val = arg;
    }
    public String toString() {
        return "[" + val + "]";
    }
}
class BoxPrinterTest {
    public static void main(String []args) {
        BoxPrinter<Integer> value1 = new BoxPrinter<Integer>(new Integer(10));
        System.out.println(value1);

        BoxPrinter<String> value2 = new BoxPrinter<String>("Hello world");
        System.out.println(value2);
    }
}
//Output
//[10]
//[Hello world]
```

### Generic methods
```java
import java.util.List;
import java.util.ArrayList;

class Utilities {
    public static <T> void fill(List<T> list, T val) {
        for(int i = 0; i < list.size(); i++)
            list.set(i, val);
    }
}
class UtilitiesTest {
    public static void main(String []args) {
        List<Integer> intList = new ArrayList<Integer>();
        intList.add(10);
        intList.add(20);
        System.out.println("The original list is: " + intList);
        Utilities.fill(intList, 100);
        System.out.println("The list after calling Utilities.fill() is: " + intList);           
    }
}
//Output
//The original list is: [10, 20]
//The list after calling Utilities.fill() is: [100, 100]
```

### Wilcards
```java
List<Number> intList = new ArrayList<Integer>(); //compiler error
List<?> wildCardList = new ArrayList<Integer>(); //no errors
```