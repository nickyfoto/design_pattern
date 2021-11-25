

```java
public class Rabbit implements Cloneable {

    public enum Breed {
        HIMALAYAN,
        AMERICAN,
        MINI_REX,
        LIONHEAD,
        DUTCH
    }

    //Age in months
    private int age;
    private Breed breed;

    public Rabbit() {
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }

    public void setBreed(Breed breed) {
        this.breed = breed;
    }

    public Breed getBreed() {
        return breed;
    }

    @Override
    public Rabbit clone() {
        try {
            return (Rabbit) super.clone();
        } catch (CloneNotSupportedException ex) {
            throw new AssertionError();
        }
    }

}


public class Main {
    public static void main(String[] args) {
        Rabbit rabbit = new Rabbit();
        rabbit.setAge(8);
        Rabbit rabbitCopy = rabbit.clone();
        System.out.println("Age of first rabbit: " + rabbit.getAge());
        System.out.println("Age of second rabbit: " + rabbitCopy.getAge());
    }    
    
}
```

Dealing with mutability

```java

public class Person implements Cloneable{

    private String name;

    public Person(String name) {

        this.name = name;

    }

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

   @Override
   public Person clone() {
       try {
           return (Person) super.clone();
       } catch (CloneNotSupportedException e) {
           throw new AssertionError();
       }
   }

}


public class Rabbit implements Cloneable {
    
    public enum Breed {
        HIMALAYAN,
        AMERICAN,
        MINI_REX,
        LIONHEAD,
        DUTCH
    }

    //Age in months
    private int age;
    private Breed breed;
    private Person owner;

    
    public Rabbit() {
        
    }

    
    public void setOwner(String name) {
        Person owner = new Person(name);
        this.owner = owner;
    }

    public Person getOwner() {
        return owner;
    }
    
        public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }

    public void setBreed(Breed breed) {
        this.breed = breed;
    }

    public Breed getBreed() {
        return breed;
    }

    
    @Override
    public Rabbit clone() {
        try {
            Rabbit rabbit = (Rabbit) super.clone();
            rabbit.owner = owner.clone();
            return rabbit;
        } catch (CloneNotSupportedException e) {
            throw new AssertionError();
        }
    }
    
}

public class Main {
    
    public static void main(String[] args) {        
        Rabbit rabbit = new Rabbit();
        rabbit.setOwner("Sally");
        Rabbit rabbitCopy = rabbit.clone();
        System.out.println("Name of first owner " + rabbit.getOwner().getName());
        System.out.println("Name of first owner " + rabbitCopy.getOwner().getName());        
       rabbitCopy.getOwner().setName("Steve");
       System.out.println(rabbit.getOwner().getName());
       System.out.println(rabbitCopy.getOwner().getName());
    }
                
}
```