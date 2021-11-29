```java

public interface Payee {

  void payExpenses(int amount);

}


public class SalesTeam implements Payee {

  private List<Payee> payees = new ArrayList<>();

  public void payExpenses(int amount) {
    payees.forEach(payee -> payee.payExpenses(amount));
  }

  void addTeamMember(Payee payee) {
    payees.add(payee);
  }

}


public class Salesperson implements Payee {

  private String name;
  private Manager manager;

  public Salesperson(String name, Manager manager) {
    this.name = name;
    this.manager = manager;
  }

  public void payExpenses(int amount) {
    System.out.println(name + " has been paid $" + amount);
  }


}


public class Manager implements Payee {

  private String name;

  public Manager(String name) {
    this.name = name;
  }

  public void payExpenses(int amount) {
    System.out.println(name + " has been paid $" + amount);
  }

}


public class ExpensesPayer {

  public static void main(String[] args) {
    Manager jane = new Manager("Jane");
    Salesperson bob = new Salesperson("Bob", jane);
    Salesperson sue = new Salesperson("Sue", jane);


    SalesTeam team = new SalesTeam();
    team.addTeamMember(jane);
    team.addTeamMember(bob);
    team.addTeamMember(sue);

    payPayee(jane, 100);
    payPayee(bob, 300);
    payPayee(team, 200);

  }

  private static void payPayee(Payee payee, int amount) {
    System.out.println("Expenses have been requested");
    payee.payExpenses(amount);
    System.out.println("Expenses have been paid\n");
  }

}

```