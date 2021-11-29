```java

public interface DisplayObject {

  void display();

}


public class ImageFile implements DisplayObject {

  BufferedImage image;

  public ImageFile(String path) {
    image = load(path);
  }

  public void display() {
    ImageIcon icon = new ImageIcon(image);
    JLabel label = new JLabel(icon);
    JOptionPane.showMessageDialog(null, label);
  }

  BufferedImage load(String path) {
    BufferedImage image = null;
    try {
      image = ImageIO.read(new File(path));
    } catch (IOException e) {
      e.printStackTrace();
    }
    return image;
  }


}



public class ImageGallery {

  public static void main(String[] args) {

    DisplayObject image1 = new ImageFile("src/main/resources/image1.jpeg");
    DisplayObject image2 = new ImageFile("src/main/resources/image2.jpeg");
    DisplayObject image3 = new ImageFile("src/main/resources/image3.jpeg");
    DisplayObject image4 = new ImageFile("src/main/resources/image4.jpeg");
    DisplayObject image5 = new ImageFile("src/main/resources/image5.jpeg");
    DisplayObject image6 = new ImageFile("src/main/resources/image6.jpeg");
    DisplayObject image7 = new ImageFile("src/main/resources/image7.jpeg");
    DisplayObject image8 = new ImageFile("src/main/resources/image8.jpeg");
    DisplayObject image9 = new ImageFile("src/main/resources/image9.jpeg");
    DisplayObject image10 = new ImageFile("src/main/resources/image10.jpeg");

    image1.display();
    image2.display();
    image3.display();
    image4.display();
    image5.display();
    image6.display();
    image7.display();
    image8.display();
    image9.display();
    image10.display();

    image1.display();
    image2.display();
    image3.display();
    image4.display();
    image5.display();
    image6.display();
    image7.display();
    image8.display();
    image9.display();
    image10.display();

  }

}

```


```java

public class ImageProxy implements DisplayObject {

  String path;
  ImageFile imageFile;

  public ImageProxy(String path) {
    this.path = path;
  }

  public void display() {
    if(imageFile == null) {
      imageFile = new ImageFile(path);
    }
    imageFile.display();
  }
}


public class ImageGallery {

  public static void main(String[] args) {

    DisplayObject image1 = new ImageProxy("src/main/resources/image1.jpeg");
    DisplayObject image2 = new ImageProxy("src/resources/image2.jpeg");
    DisplayObject image3 = new ImageProxy("src/resources/image3.jpeg");
    DisplayObject image4 = new ImageProxy("src/resources/image4.jpeg");
    DisplayObject image5 = new ImageProxy("src/resources/image5.jpeg");
    DisplayObject image6 = new ImageProxy("src/resources/image6.jpeg");
    DisplayObject image7 = new ImageProxy("src/resources/image7.jpeg");
    DisplayObject image8 = new ImageProxy("src/resources/image8.jpeg");
    DisplayObject image9 = new ImageProxy("src/resources/image9.jpeg");
    DisplayObject image10 = new ImageProxy("src/resources/image10.jpeg");

    image1.display();
    image2.display();
    image3.display();
    image4.display();
    image5.display();
    image6.display();
    image7.display();
    image8.display();
    image9.display();
    image10.display();

    image1.display();
    image2.display();
    image3.display();
    image4.display();
    image5.display();
    image6.display();
    image7.display();
    image8.display();
    image9.display();
    image10.display();

  }

}

```