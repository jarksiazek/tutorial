# Example2 

###Factory
```java
public abstract class Factory {
    public abstract InfantryUnit createInfantryUnit();     
    public abstract MechanizedUnit createMechanizedUnit();     
}    
```

###UnitFactory
```java
public class UnitFactory extends Factory {

    @Override
    public InfantryUnit createInfantryUnit() {
        new InfantryUnit();
    }

    @Override
    public MechanizedUnit createMechanizedUnit() {
        new MechanizedUnit();
    }       
}    
```

###InfantryUnit
```java
abstract class InfantryUnit {
    private int hp;
    private int exp;
}    
```

###MechanizedUnit
```java
abstract class MechanizedUnit {
    private int hp;
    private int exp;
}    
```

###Rifleman
```java
class Rifleman extends InfantryUnit {
}    
```

###Tank
```java
class Tank extends MechanizedUnit {
}    
```