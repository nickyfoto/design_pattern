



```java

public class Customer {

  private String address;

  public Customer(String address) {
    this.address = address;
  }

  public String getAddress() {
    return address;
  }

}


public class Driver {

  public void deliver(String item, int amount, Customer customer) {
    System.out.println(amount + " " + item + " out for delivery to " + customer.getAddress());
  }

}


public class ECommerceSite {

  private HashMap<String, Integer> stock;


  public ECommerceSite() {
    stock = new HashMap();
    stock.put("pens", 100);
    stock.put("pencils", 50);
    stock.put("paper", 500);
  }

  public void sell(String item, int amount) {
    int newAmount = stock.get("pens") - amount;
    stock.put(item, newAmount);
  }

  public boolean checkInStock(String item, int amount) {
    if (stock.containsKey(item) && stock.get(item) > amount) {
      return true;
    } else {
      return false;
    }
  }

}

public class Mediator {

  private Customer customer;
  private ECommerceSite site;
  private Driver driver;

  public Mediator() {
    customer = new Customer("123 Sunny Street");
    site = new ECommerceSite();
    driver = new Driver();
  }

  public void buy(String item, int amount) {
    if(site.checkInStock(item, amount)) {
      site.sell(item, amount);
      driver.deliver(item, amount, customer);
    }
  }

}


public class Main {

  public static void main(String[] args) {

    Mediator mediator = new Mediator();
    mediator.buy("pens", 3);

  }


}

```