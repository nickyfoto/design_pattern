



```java
public class Document {

  public void save() {
    System.out.println("Saving document...");
  }

  public void print() {
    System.out.println("Printing document...");
  }


}


public class Button {

  String text;

  public Button(String text) {
    this.text = text;
  }

  public void click(Command command) {
    command.execute();
  }


}


public interface Command {

   void execute();

}



public class PrintCommand implements Command {

  private Document document;

  public PrintCommand(Document document) {
    this.document = document;
  }

  public void execute() {
    document.print();
  }

}

public class SaveCommand implements Command {

  private Document document;

  public SaveCommand(Document document) {
    this.document = document;
  }

  public void execute() {
    document.save();
  }

}



public class GUI {

  private static Document document = new Document();

  public static void main(String[] args) {

    Button saveButton = new Button("Save");
    Button printButton = new Button("Print");
    // client does not know what happens when button is clicked
    // this way the framework can be used in other application as well
    // decouple the backend functionality from the frontend
    saveButton.click(new SaveCommand(document));
    printButton.click(new PrintCommand(document));

  }


}

```