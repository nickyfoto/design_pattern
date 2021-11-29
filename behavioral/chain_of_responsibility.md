



```java

public abstract class DocumentHandler {

  private DocumentHandler next;

  public DocumentHandler(DocumentHandler next) {
    this.next = next;
  }

  void openDocument(String fileExtension) {
    if(next != null) {
      next.openDocument(fileExtension);
    }
  }

}


public class SlideshowHandler extends DocumentHandler {

  public SlideshowHandler(DocumentHandler handler) {
    super(handler);
  }

  void openDocument(String fileExtension) {
    if(fileExtension.equals("ppt")) {
      System.out.println("Opening slideshow document");
    } else {
      super.openDocument(fileExtension);
    }
  }

}


public class SpreadsheetHandler extends DocumentHandler {

  public SpreadsheetHandler(DocumentHandler handler) {
    super(handler);
  }

  void openDocument(String fileExtension) {
    if(fileExtension.equals("xlsx")) {
      System.out.println("Opening spreadsheet document");
    } else {
      super.openDocument(fileExtension);
    }
  }

}


public class TextDocumentHandler extends DocumentHandler {

  public TextDocumentHandler(DocumentHandler handler) {
    super(handler);
  }

  void openDocument(String fileExtension) {
    if(fileExtension.equals("txt")) {
      System.out.println("Opening text document");
    } else {
      super.openDocument(fileExtension);
    }
  }

}


public class Client {

  public static void main(String[] args) {
    DocumentHandler chain = new SlideshowHandler(new SpreadsheetHandler(new TextDocumentHandler(null)));
    chain.openDocument("ppt");
    chain.openDocument("txt");
  }

}
```
