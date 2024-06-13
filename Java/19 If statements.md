# If Statements

``` java 
public class Main {
    public static void main(String[] args) {
        int temperature = 22;
        if (temperature > 30) {
            System.out.println("It's a hot day");
            System.out.println("Drink water");
        }
        else if (temperature > 20)
            //no need to use curly braces if there is only one statement
            System.out.println("Beautiful day");
        else {
            System.out.println("Cold day");
        }
    }
}
```

## Simplifying If statements

- We can't declare variable without having code blocks. It means we need to declare variable inside the `{}`
  ``` java 
  public class Main {
    public static void main(String[] args) {
      int income = 120_000;
      if (income > 100_000)
          //Declaration not allowed
          boolean hasHighIncome = true;
      }
  }
  ```
- If we declare variable inside the "if block", we couldn't access it out side the "if block".
  ``` java 
  public class Main {
      public static void main(String[] args) {
          int income = 120_000;
          if (income > 100_000) {
              //`hasHighIncome` is only accessible within the `if` block
              boolean hasHighIncome = true;
          }
          //"hasHighIncome" is not accessible here
          //Compilation error
          System.out.println(hasHighIncome);
      }
  }
  ```
- We can declare variable outside the if block.
  ``` java 
  public class Main {
      public static void main(String[] args) {
          int income = 120_000;
          boolean hasHighIncome;
          if (income > 100_000)
              hasHighIncome = true;
          else
              hasHighIncome = false;
      }
  }
  ```
- We can improve this code and remove "else" part
  ```java 
  public class Main {
      public static void main(String[] args) {
          int income = 120_000;
          boolean hasHighIncome= false;
          if (income > 100_000)
              hasHighIncome = true;
      }
  }
  ```
- Ultimate version of the code
  ``` java 
  public class Main {
      public static void main(String[] args) {
          int income = 120_000;
          boolean hasHighIncome= (income > 100_000);
      }
  }
  ```