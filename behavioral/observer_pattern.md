


```java

import java.beans.PropertyChangeEvent;
import java.beans.PropertyChangeListener;
import java.util.ArrayList;

public class SocialMediaFeed implements PropertyChangeListener {

  private ArrayList<String> statuses = new ArrayList<>();

  public void printStatuses() {
    statuses.forEach(System.out::println);
  }

  public void propertyChange(PropertyChangeEvent event) {
    statuses.add((String) event.getNewValue());
  }

}


import java.beans.PropertyChangeListener;
import java.beans.PropertyChangeSupport;

public class Connection {

  private PropertyChangeSupport support = new PropertyChangeSupport(this);
  private String status = "";

  public void addPropertyChangeListener(PropertyChangeListener listener) {
    support.addPropertyChangeListener(listener);
  }

  public void setStatus(String status) {
    support.firePropertyChange("status", this.status, status);
    this.status = status;
  }

}


public class Main {

  public static void main(String[] args) {
    Connection observable = new Connection();
    Connection observable2 = new Connection();
    SocialMediaFeed observer = new SocialMediaFeed();

    observable.addPropertyChangeListener(observer);
    observable2.addPropertyChangeListener(observer);
    observable.setStatus("going for a walk");
    observable2.setStatus("eating my lunch");

    observer.printStatuses();


  }


}

```