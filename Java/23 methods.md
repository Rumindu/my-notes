# Methods
``` java 
public class Main {
    //main method
    public static void main(String[] args) {
      //calling the "greetUser" method
      greetUser("Rumindu");
    }
    // "greetUser" method
    //"static" means method belongs to the class not for the object/ instence of a class
    //void means method does not return a value
    // "name" is a parameter
    public static void greetUser(String name) {
      System.out.println("Hello "+ name);
    }
}
```
- We can reuse `greetUser` method. 
  ``` java
  public static void main(String[] args) {
          greetUser("Kavishka");
          greetUser("Rumindu");
      }
  ```
- Method with multiple parameters
  ``` java 
  public class Main {
      public static void main(String[] args) {
          //Here order of the arguments is important
          greetUser("Rumindu", "Ranaweera");
          greetUser("Kavishka", "Ranaweera");
      }
      public static void greetUser(String firstName, String lastName) {
          System.out.println("Hello "+ firstName + " " + lastName);
      }
  }
  ```
- Method which returns a value
  ``` java 
  public class Main {
      public static void main(String[] args) {
          //assign returning values of method to the "message" variable
          String message=greetUser("Rumindu", "Ranaweera");
          System.out.println(message);
      }
      //Here replace "void" by "String" to return a string value
      public static String greetUser(String firstName, String lastName) {
          return ("Hello "+ firstName + " " + lastName);
      }
  }
  ```