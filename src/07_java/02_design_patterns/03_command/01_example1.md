### Example1
* implementation is done, focusing on sending different objects

### Interface
```java
public interface Command {
    void execute();
}
```

### Robot
```java
public class Robot {
    void turnOn(){
        System.out.println("Robot turn on");
    } 

    void turnOff(){
        System.out.println("Robot turn off");
    } 
}
```

### TurnOnCommand
```java
public class TurnOnCommand implements Command {
    private Robot robot;

    public TurnOnCommand (Robot robot) {
        this.robot = robot;        
    }   

    void execute() {
        this.robot.turnOn();
    }
}
```

### TurnOffCommand
```java
public class TurnOffCommand implements Command {
    private Robot robot;

    public TurnOffCommand (Robot robot) {
        this.robot = robot;        
    }   

    void execute() {
        this.robot.turnOff();
    }
}
```

### Workshop
```java
import java.util.ArrayList;
public class Workshop {
    private List<Command> commandQueue = new ArrayList<>();

    public void addToQueue(Command command){
        commandQueue.add(command);
    }
    
      public void run(){
            commandQueue.forEach(
                command -> command.execute()
            );              
        }
}
```

### Main
```java
public class Main {
    public static void main(String[] args){
        Robot robot = new Robot();
        Workshop workshop = new Workshop();
        workshop.addToQueue(new TurnOnCommand(robot));
        workshop.addToQueue(new TurnOffCommand(robot));
        
        workshop.run();
    }
}
```