### Example2

```java
public interface MusicPlayerCommand  {
    void play();
}
```

```java
public class MusicPlayerRemote {
    private MusicPlayerCommand musicPlayerCommand;

    public MusicPlayerRemote (MusicPlayerCommand musicPlayerCommand) {
        this.musicPlayerCommand = musicPlayerCommand;        
    }       
    
    void pressButton(){
        musicPlayerCommand.play();
    }
}
```

```java
public class MusicPlayer {
    private List<String> tracks = Arrays.asList("Track1","Track2","Track3");
    private int currentTrackNumber;    

    void playFist(){
        System.out.println(tracks.get(0));
    }    
    void playFist(){
        currentTrackNumber++;
        if (currentTrackNumber > tracks.size())
            currentTrackNumber = 0;       
        System.out.println(tracks.get(currentTrackNumber));

    }
    void playRandomTrack(){        
        System.out.println(tracks.get(rand.nextInt(tracks.size())));
    }
}
```

```java
public class MusicPlayerPlayFirstTrack implements MusicPlayerCommand {
    private MusicPlayerPlay musicPlayerPlay;

    public MusicPlayerPlayFirstTrack (MusicPlayer musicPlayer) {
        this.robot = robot;        
    } 

    void play(){
        this.musicPlayerPlay.playFirst();     
    }
}
```

### Main
```java
public class Main {
    public static void main(String[] args){
        MusicPlayerPlay musicPlayerPlay = new MusicPlayerPlay();
        MusicPlayerRemote musicPlayerRemote = new MusicPlayerRemote(new MusicPlayerPlayFirstTrack());
        musicPlayerRemote.pressButton();
    }
}
```