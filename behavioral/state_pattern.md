```java

public interface State {

  void pause(MediaPlayer player);
  void play(MediaPlayer player);

}

public class PlayingState implements State {

  public void pause(MediaPlayer player) {
    player.setState(new PausedState());
    player.setIcon("play button");
    System.out.println("Video paused, icon set to " + player.getIcon());
   }

  public void play(MediaPlayer player) {
    // do nothing
  }

}


public class PausedState implements State {

  public void pause(MediaPlayer player) {
    // do nothing
  }

  public void play(MediaPlayer player) {
    player.setState(new PlayingState());
    player.setIcon("pause button");
    System.out.println("Video playing, icon set to " + player.getIcon());
  }


}


public class MediaPlayer {

  private State state = new PausedState();
  private String icon = "play button";

  public void setState(State state) {
    this.state = state;
  }

  public State getState() {
    return state;
  }

  public String getIcon() {
    return icon;
  }

  public void setIcon(String icon) {
    this.icon = icon;
  }

  public void play() {
    getState().play(this);
  }

  public void pause() {
    getState().pause(this);
  }

}


public class Main {

  public static void main(String[] args) {
    MediaPlayer mediaPlayer = new MediaPlayer();
    mediaPlayer.play();
    mediaPlayer.pause();
  }

}

```