```java


public class Adapter implements PriceCalculator {

  UKCarPriceCalculator calculator;

  public Adapter(UKCarPriceCalculator calculator) {
    this.calculator = calculator;
  }

  @Override
  public String calculatePrice() {
    return calculator.getPrice() + "GBP";
  }
}


public interface PriceCalculator {

  String calculatePrice();

}


public class CarPriceCalculator implements PriceCalculator {

  private int age;
  private String model;
  public static int averageCarPrice = 6000;

  public CarPriceCalculator(String model, int age) {
    this.model = model;
    this.age = age;
  }

  public int getRetailPrice() {
    switch (model) {
      case "Ford":
        return 3000;
      case "Audi":
        return 5000;
      case "BMW":
        return 7000;
      case "Tesla":
        return 10000;
      default:
        return averageCarPrice;
    }
  }

  @Override
  public String calculatePrice() {
    int price = Math.max(getRetailPrice() - (age * 100), 0);
    return price + "USD";
  }

}


public class TruckPriceCalculator implements PriceCalculator {

  private int age;
  private int mileage;
  public static int averagePrice = 10000;

  public TruckPriceCalculator(int age, int mileage) {
    this.age = age;
    this.mileage = mileage;
  }

  @Override
  public String calculatePrice() {
    int price = Math.max(averagePrice - age*100 - mileage/100, 0);
    return price + "USD";
  }

}


public class Main {

  public static void main(String[] args) {
    CarPriceCalculator carPriceCalculator = new CarPriceCalculator("Ford", 3);
    printVehiclePrice(carPriceCalculator);

    TruckPriceCalculator truckPriceCalculator = new TruckPriceCalculator(10, 0);
    printVehiclePrice(truckPriceCalculator);

    UKCarPriceCalculator UKCarPriceCalculator = new UKCarPriceCalculator("BMW", 7);
    Adapter adapter = new Adapter(UKCarPriceCalculator);
    printVehiclePrice(adapter);
  }

  public static void printVehiclePrice(PriceCalculator calculator) {
    String price = calculator.calculatePrice();
    System.out.println("The price of vehicle is: " + price);
  }

}

```