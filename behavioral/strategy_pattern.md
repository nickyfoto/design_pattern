


```java

public interface Encryptor {

  String encryptFile();
  // Java 8 static method in interface
  Encryptor aesEncryptor = () -> "Applying AES encryption";
  Encryptor rsaEncryptor = () -> "Applying RSB encryption";

}

public class File {

  private String fileName;

  public File(String fileName) {
    this.fileName = fileName;
  }

  public void encrypt(Encryptor encryptor) {
    System.out.println(encryptor.encryptFile() + " to " + fileName);
  }

}




public class Main {

  public static void main(String[] args) {
    File file = new File("test.pdf");
    file.encrypt(Encryptor.aesEncryptor);
  }

}

```