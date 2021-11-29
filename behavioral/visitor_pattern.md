

```java





public interface Visitor {

  void visit(Bread bread);
  void visit(Milk milk);
  void visit(GroceryList groceryList);

}


public class DiscountVisitor implements Visitor {

  public void visit(Bread bread) {
    bread.setPrice(0.9);
  }

  public void visit(Milk milk) {
    milk.setPrice(1.6);
  }

  public void visit(GroceryList groceryList) {
    System.out.println("Discounts have been applied to your grocery list");
  }

}

public interface Groceries {

  double getPrice();
  void accept(Visitor visitor);

}

public class GroceryList implements Groceries {

  ArrayList<Groceries> groceries = new ArrayList<Groceries>();

  public GroceryList() {
    Bread bread = new Bread();
    Bread bread2 = new Bread();
    Milk milk = new Milk();
    groceries.add(bread);
    groceries.add(milk);
    groceries.add(bread2);
  }

  public double getPrice() {
    return groceries.stream().mapToDouble(Groceries::getPrice).sum();
  }

  public void accept(Visitor visitor) {
    groceries.forEach(g -> g.accept(visitor));
    visitor.visit(this);
  }
}



public class Client {

  public static void main(String[] args) {
    GroceryList groceryList = new GroceryList();
    System.out.println("Total price of grocery list: " + groceryList.getPrice());
    groceryList.accept(new DiscountVisitor());
    System.out.println("New total price of grocery list: " + groceryList.getPrice());
  }

}


```