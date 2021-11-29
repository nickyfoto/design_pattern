

```java

public interface Expression {

  String interpret(String context);

}

public class NameNotPrimitiveType implements Expression {

  public String interpret(String context) {
    if(context.equals("int") || context.equals("boolean") || context.equals("double")) {
      context = context + "1";
    }
    return context;
  }

}


public class FirstLetterIsLowerCase implements Expression {

  private NameNotPrimitiveType nameNotPrimitiveType = new NameNotPrimitiveType();

  public String interpret(String context) {

    context = context.substring(0,1).toLowerCase() + context.substring(1);
    return nameNotPrimitiveType.interpret(context);


  }
}


public class FirstLetterNotUnderscore implements Expression {

  private FirstLetterIsLowerCase firstLetterIsLowerCase = new FirstLetterIsLowerCase();

  public String interpret(String context) {
    if(context.startsWith("_")) {
      context = context.substring(1);
    }
    return firstLetterIsLowerCase.interpret(context);
  }
}

public class Main {

  public static void main(String[] args) {

    String context = "_Int";
    FirstLetterNotUnderscore firstLetterNotUnderscore = new FirstLetterNotUnderscore();
    context = firstLetterNotUnderscore.interpret(context);
    System.out.println(context);
  }

}

```