```java

public class PrintSpooler {
    
    private static PrintSpooler spooler;
    
    private static boolean initialized = false;
    
    private PrintSpooler(){}
    
    private void init() {
        // Code to initialize our print spooler goes here
    }
    
    public static PrintSpooler getInstance() {
        
        if(initialized) return spooler;
        spooler = new PrintSpooler();
        spooler.init();
        initialized = true;
        return spooler;
                
    }            
       
}



public class ResourceManager {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {            
        // instead of using new the private method in PrintSpooler
        // prevents it and client can only use the getInstance method
        PrintSpooler spooler = PrintSpooler.getInstance();
                          
    }

}

```

Thread safe singleton

```java

public class PrintSpooler {
    
    private static final PrintSpooler spooler = new PrintSpooler();
    
    private static boolean initialized = false;
    
    private PrintSpooler(){}
    
    private void init() {
        // Code to initialize our printer spooler goes here
    }
    
    public static synchronized PrintSpooler getInstance() {
        
        if(initialized) return spooler;
        spooler.init();
        initialized = true;
        return spooler;
                
    }            
    
}

public class ResourceManager {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {            

        PrintSpooler spooler = PrintSpooler.getInstance();
        
        // First thread        
        Thread threadOne = new Thread(() -> {PrintSpooler s = PrintSpooler.getInstance();});
        
        // Second thread
        Thread threadTwo = new Thread(() -> {PrintSpooler s = PrintSpooler.getInstance();});
        
        threadOne.start();        
        threadTwo.start();                            

    }

}
```

Here we move the initialization from the `getInstance` method to when we declare the field. This prevents that even if we do not use the `synchronized` keyword, still only one instance can be created. This is because the object is created before the `getInstance` method is being called.


https://www.geeksforgeeks.org/collections-singletonlist-method-in-java-with-examples/

The singletonList() method of java.util.Collections class is used to return an immutable list containing only the specified object. The returned list is serializable. This list will always contain only one element thus the name singleton list. When we try to add/remove an element on the returned singleton list, it would give UnsupportedOperationException.

