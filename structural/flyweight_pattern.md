


```java

public class Car implements Vehicle {

  private int[] location = new int[2];

  public String getType() {
    return "Car";
  }

  public void setLocation(int latitude, int longitude) {
    location[0] = latitude;
    location[1] = longitude;
  }

  public int[] getLocation() {
    return location;
  }

}


public interface Vehicle {

  String getType();
  int[] getLocation();
  void setLocation(int latitude, int longitude);
}

public class Truck implements Vehicle {

  private int[] location = new int[2];

  public String getType() {
    return "Truck";
  }

  public void setLocation(int latitude, int longitude) {
    location[0] = latitude;
    location[1] = longitude;
  }

  public int[] getLocation() {
    return location;
  }

}


public class TrafficSimulator {

  static ArrayList<Vehicle> vehicles = new ArrayList();

  public static void main(String[] args) {

    Runnable createVehicles = new Runnable() {
      public void run() {
        createRandomCar();
      }
    };

    Runnable removeVehicles = new Runnable() {
      public void run() {
        removeCar();
      }
    };

    ScheduledExecutorService executor = Executors.newScheduledThreadPool(1);
    executor.scheduleAtFixedRate(createVehicles, 0, 3, TimeUnit.SECONDS);
    executor.scheduleAtFixedRate(removeVehicles, 5, 5, TimeUnit.SECONDS);
  }

  private static void createRandomCar() {
    Random random = new Random();
    int randInt = random.nextInt(2);
    Vehicle vehicle = null;
    if(randInt == 0) {
      vehicle = new Car();
    } else if(randInt == 1) {
      vehicle = new Truck();
    }
    vehicle.setLocation(random.nextInt(1000), random.nextInt(1000));
    System.out.println("Creating " + vehicle + ", type: " + vehicle.getType() +
        ", location: " + vehicle.getLocation()[0] + " " + vehicle.getLocation()[1]);
    vehicles.add(vehicle);
  }

  private static void removeCar() {
    System.out.println("Removing " + vehicles.get(0));
    vehicles.remove(0);
  }

}

```


```java

public class VehicleFactory {

  private HashMap<Integer, Vehicle> vehicles = new HashMap<>();

  public Vehicle getVehicle(int type) {
    if(vehicles.containsKey(type)) {
      return vehicles.get(type);
    } else {
      Vehicle vehicle = null;
      if(type == 0) {
        vehicle = new Car();
      } else if(type == 1) {
        vehicle = new Truck();
      }
      vehicles.put(type, vehicle);
      return vehicle;
    }
  }

}


public class TrafficSimulator {

  static ArrayList<Vehicle> vehicles = new ArrayList();
  static VehicleFactory vehicleFactory = new VehicleFactory();

  public static void main(String[] args) {

    Runnable createVehicles = new Runnable() {
      public void run() {
        createRandomCar();
      }
    };

    Runnable removeVehicles = new Runnable() {
      public void run() {
        removeCar();
      }
    };

    ScheduledExecutorService executor = Executors.newScheduledThreadPool(1);
    executor.scheduleAtFixedRate(createVehicles, 0, 3, TimeUnit.SECONDS);
    executor.scheduleAtFixedRate(removeVehicles, 3, 5, TimeUnit.SECONDS);
  }

  private static void createRandomCar() {
    Random random = new Random();
    int randInt = random.nextInt(2);
    Vehicle vehicle = vehicleFactory.getVehicle(randInt);
    vehicle.setLocation(random.nextInt(1000), random.nextInt(1000));
    System.out.println("Creating " + vehicle + ", type: " + vehicle.getModel() +
        ", location: " + vehicle.getLocation()[0] + " " + vehicle.getLocation()[1]);
    vehicles.add(vehicle);
  }

  private static void removeCar() {
    System.out.println("Removing " + vehicles.get(0));
    vehicles.remove(0);
  }

}

```