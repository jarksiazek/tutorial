### Example1

### Interface
```java
class EggCooker {
    void cookEgg();
}
```
### EggCooker1
```java
class HardBoiledEggCooker implements EggCooker {
    void cookEgg(){
        System.out.println("HardBoiledEggs");
    }
}
```

### EggCooker2
```java
class SoftBoiledEggCooker implements EggCooker {
    void cookEgg(){
        System.out.println("SoftBoiledEggs");
    }
}
```

### Implementation
```java
class Cooker {
    private EggCooker eggCooker;

    public cook() {
        this.eggCooker.cookEgg();
    }
    
    void setEggCooker(EggCooker eggCooker) {
        this.eggCooker = eggCooker;
    } 
}
```

### Main
```java
class Main {
    public static void main(String[] args){
        Chef chef = new Chef();
        chef.setEggCooker(new HardBoiledEggCooker);
        chef.cookEgg();
        //print HardBoiledEggs

        chef.setEggCooker(new HardBoiledEggCooker);
        chef.cookEgg();
        //print HardBoiledEggs
    }
}
```