



```java
public abstract class Pizza {

  public void makeBase() {
    System.out.println("Mix flour, yeast and salt");
    System.out.println("Roll out the dough");
  }

  public void addToppings(){
    System.out.println("Add tomato");
    System.out.println("Add cheese");
  }

  public void cook(){}

}


public class VegetarianPizza extends Pizza {

  public void addToppings() {
    super.addToppings();
    System.out.println("Add peppers");
    System.out.println("Add olives");
  }

  public void cook() {
    System.out.println("Cook in the oven for 15 minutes");
  }


}

public class MeatFeastPizza extends Pizza {

  public void addToppings() {
    super.addToppings();
    System.out.println("Add pepperoni");
    System.out.println("Add ham");
    System.out.println("Add chicken");
  }

  public void cook() {
    System.out.println("Cook in the oven for 20 minutes");
  }

}



public class Main {

  public static void main(String[] args) {
    VegetarianPizza vegetarian = new VegetarianPizza();
    vegetarian.makeBase();
    vegetarian.addToppings();
    vegetarian.cook();

    System.out.println();

    MeatFeastPizza meatFeast = new MeatFeastPizza();
    meatFeast.makeBase();
    meatFeast.addToppings();
    meatFeast.cook();
  }

}

```