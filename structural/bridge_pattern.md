


```java

public abstract class Shape {

  abstract public void draw(Graphics graphics);

}


public class Square extends Shape {

  ColorShape colorShape;

  public Square(ColorShape colorShape) {
    this.colorShape = colorShape;
  }

  public void draw(Graphics graphics) {
    colorShape.setColor(graphics);
    graphics.fillRect(5, 15, 50, 50);
  }

}

public class Circle extends Shape{

  ColorShape colorShape;

  public Circle(ColorShape colorShape) {
    this.colorShape = colorShape;
  }

  public void draw(Graphics graphics) {
    colorShape.setColor(graphics);
    graphics.fillOval(75, 15, 50, 50);
  }



}


public class Triangle extends Shape {

  ColorShape colorShape;

  public Triangle(ColorShape colorShape) {
    this.colorShape = colorShape;
  }

  public void draw(Graphics graphics) {
    colorShape.setColor(graphics);
    int[] x = {200, 250, 150};
    int[] y = {15, 65, 65};
    int n = 3;
    graphics.fillPolygon(x, y, n);
  }

}
```

```java
public interface ColorShape {

  void setColor(Graphics graphics);

}


public class BlueColorShape implements ColorShape {

  public void setColor(Graphics graphics) {
    graphics.setColor(Color.BLUE);
  }

}

public class RedColorShape implements ColorShape {

  public void setColor(Graphics graphics) {
    graphics.setColor(Color.RED);
  }

}

public class GreenColorShape implements ColorShape {

  public void setColor(Graphics graphics) {
    graphics.setColor(Color.GREEN);
  }

}


public class Canvas extends JPanel {


  public static void main(String[] a) {
    // Creates a canvas to draw on
    JFrame frame = new JFrame();
    frame.setSize(400, 400);
    frame.add(new Canvas());
    frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    frame.setVisible(true);
  }


  public void paint(Graphics graphics) {
    Square square = new Square(new BlueColorShape());
    square.draw(graphics);
    Circle circle = new Circle(new RedColorShape());
    circle.draw(graphics);
    Triangle triangle = new Triangle(new GreenColorShape());
    triangle.draw(graphics);
  }

}


```