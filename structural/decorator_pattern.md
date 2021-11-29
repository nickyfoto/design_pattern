
```java

public interface Component {

  void draw(Graphics graphics);

}


public class Circle implements Component {

  private int x;
  private int y;

  public Circle(int x, int y) {
    this.x = x;
    this.y = y;
  }

  public void draw(Graphics graphics) {
    graphics.drawOval(x, y, 50, 50 );
  }

}

public class ComponentWithRedBorder implements Component {

  private Component decoratedComponent;

  public ComponentWithRedBorder(Component component) {
    this.decoratedComponent = component;
  }

  public void draw(Graphics graphics) {
    graphics.setColor(Color.RED);
    decoratedComponent.draw(graphics);
    graphics.setColor(Color.BLACK);
  }


}


public class Canvas extends JPanel {

  Component circle1 = new Circle(15, 15);
  Component circle2 = new Circle(75, 15);
  Component circle3 = new Circle(135, 15);

  public static void main(String[] args) {
    // Creates a canvas to draw on
    JFrame frame = new JFrame();
    frame.setSize(400, 400);
    frame.add(new Canvas());
    frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    frame.setVisible(true);
  }

  public void paint(Graphics graphics) {
    circle1.draw(graphics);
    circle2 = new ComponentWithRedBorder(circle2);
    circle2.draw(graphics);
    circle3.draw(graphics);
  }

}

```


example 2

```java

public abstract class Pizza {
	String description = "Basic Pizza";
  
	public String getDescription() {
		return description;
	}
 
	public abstract double cost();
}


public class ThincrustPizza extends Pizza {
  
	public ThincrustPizza() {
		description = "Thin crust pizza, with tomato sauce";
	}
  
	public double cost() {
		return 7.99;
	}
}


public abstract class ToppingDecorator extends Pizza {
	Pizza pizza;
	public abstract String getDescription();
}


public class Cheese extends ToppingDecorator {
	
 
	public Cheese(Pizza pizza) {
		this.pizza = pizza;
	}
 
	public String getDescription() {
		return pizza.getDescription() + ", Cheese";
	}
 
	public double cost() {
		return pizza.cost(); // cheese is free
	}
}

public class Olives extends ToppingDecorator {
	
 
	public Olives(Pizza pizza) {
		this.pizza = pizza;
	}
 
	public String getDescription() {
		return pizza.getDescription() + ", Olives";
	}
 
	public double cost() {
		return pizza.cost() + .30; 
	}
}


public class PizzaStore {
 
	public static void main(String args[]) {
		Pizza pizza = new ThincrustPizza();
		Pizza cheesePizza = new Cheese(pizza);
		Pizza greekPizza = new Olives(cheesePizza);

		System.out.println(greekPizza.getDescription() 
				+ " $" + greekPizza.cost());

	}
}


```