
```java

public abstract class Handlebar {
    
    abstract void getDescription();
    
}

public class MountainBikeHandlebar extends Handlebar {
    
    private static String type = "FLAT";
    
    @Override
    public void getDescription() {
        System.out.println("Mountain bike handlebar. Type: " + type);
    }
    
}


public class RoadBikeHandlebar extends Handlebar {

    private static String type = "DROP";

    @Override
    public void getDescription() {
        System.out.println("Road bike handlebar. Type: " + type);
    }

}



public abstract class Tire {
    
    abstract void getDescription();
    
}


public class MountainBikeTire extends Tire {

    private static final String width = "WIDE";

    private static final String pressure = "MEDIUM";
    
    @Override
    public void getDescription() {
        System.out.println("Mountain bike tire. Width: " + width + ", pressure: " + pressure);        
    }

}


public class RoadBikeTire extends Tire {
    
    private static final String width = "NARROW";
    private static final String pressure = "HIGH";
    
    @Override
    public void getDescription() {
        System.out.println("Road bike tire width: " + width);        
    }
    
}
```

```java


public abstract class BikeFactory {        
    
    abstract Tire createTire();
    
    abstract Handlebar createHandlebar();        
    
}

public class RoadBikeFactory extends BikeFactory {
    
    @Override
    public Tire createTire() {
        return new RoadBikeTire();
    }
    
    @Override
    public Handlebar createHandlebar() {
        return new RoadBikeHandlebar();
    }
    
}


public class MountainBikeFactory extends BikeFactory {
    
    @Override
    public Tire createTire() {
        return new MountainBikeTire();
    }
    
    @Override
    public Handlebar createHandlebar() {
        return new MountainBikeHandlebar();
    }
    
}

public class FactoryCreator {
    
    public static BikeFactory createFactory(String type) {
        
        if(type.equalsIgnoreCase("mountain bike")) {
            return new MountainBikeFactory();
        } else if(type.equalsIgnoreCase("road bike")) {
            return new RoadBikeFactory();
        } else {
            System.out.println("Please specify a valid type");
            return null;
        }
        
    }
    
}


public class BikeBuilder {    

    public static void main(String[] args) {
        
        createBikeWithoutAbstractFactory();              
        // this is much better because it can easily changed to road bike
        createBikeWithAbstractFactory("mountain bike");
        
    }
    
    public static void createBikeWithoutAbstractFactory() {
        
        MountainBikeTire mountainBikeTireFront = new MountainBikeTire();
        MountainBikeTire mountainBikeTireBack = new MountainBikeTire();
        MountainBikeHandlebar mountainBikeHandlebar = new MountainBikeHandlebar();        
        mountainBikeTireFront.getDescription();
        mountainBikeTireBack.getDescription();
        mountainBikeHandlebar.getDescription();
        System.out.println();  
        
    }
    
    public static void createBikeWithAbstractFactory(String type) {
        
        BikeFactory bikeFactory = FactoryCreator.createFactory(type);        
        Tire tireFront = bikeFactory.createTire();
        Tire tireBack = bikeFactory.createTire();
        Handlebar handlebar = bikeFactory.createHandlebar();
        tireFront.getDescription();
        tireBack.getDescription();
        handlebar.getDescription();  
        System.out.println();
        
    }
    
}

```


extensible factories

```java
public abstract class Handlebar extends BikePart {
    
    @Override
    abstract void getDescription();
    
}

public abstract class Tire extends BikePart {
    
    abstract void getDescription();
    
}

public class MountainBikeHandlebar extends Handlebar {
    
    private static String type = "FLAT";
    
    @Override
    public void getDescription() {
        System.out.println("Mountain bike handlebar. Type: " + type);
    }
    
}

public class MountainBikeTire extends Tire {

    private static final String width = "WIDE";

    private static final String pressure = "MEDIUM";
    
    @Override
    public void getDescription() {
        System.out.println("Mountain bike tire. Width: " + width + ", pressure: " + pressure);        
    }

}


public class RoadBikeHandlebar extends Handlebar {

    private static String type = "DROP";

    @Override
    public void getDescription() {
        System.out.println("Road bike handlebar. Type: " + type);
    }

}


public class RoadBikeTire extends Tire {
    
    private static final String width = "NARROW";
    private static final String pressure = "HIGH";
    
    @Override
    public void getDescription() {
        System.out.println("Road bike tire width: " + width + ", pressure: " + pressure);        
    }
    
}

```




```java

abstract class BikePart {  
    
    abstract void getDescription();
    
    
}

public abstract class BikeFactory {           
    
    abstract BikePart create(String type);
    
}


public class MountainBikeFactory extends BikeFactory {
    
    @Override
    public BikePart create(String type) {
        if (type.equalsIgnoreCase("tire")) {
            return new MountainBikeTire();
        } else if (type.equalsIgnoreCase("handlebar")) {
            return new MountainBikeHandlebar();
        } else {
            return null;
        }
    }
    
}


public class RoadBikeFactory extends BikeFactory {
    // it is extensible because we can add more parts here
    @Override
    public BikePart create(String type) {
        if (type.equalsIgnoreCase("tire")) {
            return new RoadBikeTire();
        } else if (type.equalsIgnoreCase("handlebar")) {
            return new RoadBikeHandlebar();
        } else {
            return null;
        }
    }
    
}



public class FactoryCreator {
    
    public static BikeFactory createFactory(String type) {
        
        if(type.equalsIgnoreCase("mountain bike")) {
            return new MountainBikeFactory();
        } else if(type.equalsIgnoreCase("road bike")) {
            return new RoadBikeFactory();
        } else {
            System.out.println("Please specify a valid type");
            return null;
        }
        
    }
    
}


public class BikeBuilder {    

    public static void main(String[] args) {        
        
        createBikeWithExtensibleAbstractFactory("road bike");
        
    }   
    
    public static void createBikeWithExtensibleAbstractFactory(String type) {
        
        BikeFactory bikeFactory = FactoryCreator.createFactory(type); 
        Tire tireFront = (Tire) bikeFactory.create("tire");
        tireFront.getDescription();
        Tire tireBack = (Tire) bikeFactory.create("tire");
        tireBack.getDescription();
        Handlebar handlebar = (Handlebar) bikeFactory.create("handlebar");
        handlebar.getDescription();
        
    }
    
}

```
