


```java

public class Memento {

  private String state;

  public Memento(String state) {
    this.state = state;
  }

  public String getState() {
    return state;
  }

  public void setState(String state) {
    this.state = state;
  }
}


public class TextDocument {

  private String text = "";
  private Memento memento = new Memento(text);

  public void write(String text) {
    this.text += text;
  }

  public void print() {
    System.out.println(text);
  }

  public void save() {
    memento.setState(text);
  }

  public void undo() {
    text = memento.getState();
  }

}

public class DocumentViewer {

  private static TextDocument textDocument = new TextDocument();

  public static void main(String[] args) {
    textDocument.write("hello");
    textDocument.save();
    textDocument.print();
    textDocument.write(" world");
    textDocument.print();
    textDocument.undo();
    textDocument.print();
  }

}
```
