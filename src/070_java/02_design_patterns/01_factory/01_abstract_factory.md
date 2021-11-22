# Example1 

###Factory
```java
public abstract class Factory {
    public abstract Unit createUnit(UnionType unionType);     
}    
```

###UnitFactory
```java
public class UnitFactory extends Factory {

    @Override
    public Unit createUnit(UnionType unionType) {
        switch (unionType) {
            case TANK: return new Tank();
            case RIFLEMAN: return new Rifleman(); 
            default: throw new UnsupportedOperationException(); 
        }
    }     
}    
```

###Unit
```java
abstract class Unit {
    private int hp;
    private int exp;
}    
```

###Tank
```java
class Tank extends Unit {
}    
```

###Rifleman
```java
class Rifleman extends Unit {
}    
```