### interface 
* abstract class does not need to implement interface method
* cannot be initialized
* can extend other interface
* members - public static final
* 3 kinds of methods: abstract, default methods, static methods 
* can be declared without body - e.i. EventListener
* can be declared within interface(nested interface) or class (nested class)

```java
interface Rollable { 
    void roll(float degree );
}
```

### functional interface
* has only one abstract method or inherits only one abstract method.
* can have many of static or default methods
* for a functional interface, declaring methods from Object class in an interface does
not count as an abstract method.
```java
// in java.lang package
interface Runnable { void run(); }
// in java.util package
interface Comparator<T> { boolean compare(T x, T y); }
// java.awt.event package:
interface ActionListener { void actionPerformed(ActionEvent e); }
// java.io package
interface FileFilter { boolean accept(File pathName); }
```
