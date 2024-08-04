# Getters and Setters
- Previous lesson, "Encapsulation" implementation has a problem. There is no validation before assigning values to the attributes of the object.
  ``` java 
  //Main.java
  public class Main {
      public static void main(String[] args) {
          var employee = new Employee();
          // Here is the issue, we can set the baseSalary to any value
          employee.baseSalary = -1;
          employee.hourlyRate = 20;
      }
  }
  ```
- One way is add a "if condition" to validate the baseSalary.
- But the problem is every time when we use employee object we need use this if condition.
- Recommended way is we can ***encapsulate this condition inside the Employee class***.
- public - We can access outside from the class. 
	- It means we can assign or get values using `objectName.attribute/methodName`
- Private - We can't access outside from the class.
## Setter
- When we set `baseSalary` as private attribute in the "Employee" class, we couldn't assign values like `employee.baseSalary = -1;`.
- To set values we create method on the "Employee" class with validations
  ``` java 
  //Employee.java
  public class Employee {
      private int baseSalary;
      public int hourlyRate;

      public int calculateWage(int extraHours) {
          return baseSalary + (hourlyRate * extraHours);
      }
      //setter
      public void setBaseSalary(int baseSalary) {
          if (baseSalary <= 0)
              //use "throw" to raise an exception
              //If we don't handle the exception it will terminate the program
              //display exception in the console using the instance of IllegalArgumentException
              throw new IllegalArgumentException("Salary cannot be 0 or less");
          this.baseSalary = baseSalary;
      }
  }
  ```
- And we call "setBaseSalary" method in the "Main" class 
  ``` java 
  //Main.java
  public class Main {
      public static void main(String[] args) {
          var employee = new Employee();
          employee.setBaseSalary(-1);
          employee.hourlyRate = 20;
      }
  }
  ```
- When we run the Main.java with passing -1 to the setBaseSalary() we will get this exception
  ![](assets/Pasted%20image%2020240627095908.png)
## Getter
- When the property is private we couldn't get values using `objectName.prpertyName`
- For that we need a method on the "Employee" class when it calls on Main class it will return the value of the relevant attribute. This type of methods calls ***Getters***.
  ``` java 
  //Employee.java
  public class Employee {
      private int baseSalary;
      public int hourlyRate;
      public int calculateWage(int extraHours) {
          return baseSalary + (hourlyRate * extraHours);
      }
      public void setBaseSalary(int baseSalary) {
          if (baseSalary <= 0)
              //use "throw" to raise an exception and terminate the program
              //display exception in the console using the instance of IllegalArgumentException
              throw new IllegalArgumentException("Salary cannot be 0 or less");
          this.baseSalary = baseSalary;
      }

      //getter
      public int getBaseSalary() {
          return baseSalary;
      }
  }
  ```

  ``` java 
  //Main.java
  public class Main {
      public static void main(String[] args) {
          var employee = new Employee();
          employee.setBaseSalary(5000);
          //use employee.getBaseSalary() to get the value of private baseSalary
          System.out.println(employee.getBaseSalary());//
          employee.hourlyRate = 20;
      }
  }
  ```

## IntelliJ IDE short cut for create getters and setters
- Lets convert "horlyRate" as a private attribute using IntelliJ option
- Go to relevant line and click on 💡or press `alt+enter`.
 ![](assets/Pasted%20image%2020240627133428.png)
 - Then u can see this menu.
  ![](assets/Pasted%20image%2020240627133556.png)
 - From this choose "Encapsulate fields 'hourlyRate'". then you can see popup menu.
  ![](assets/Pasted%20image%2020240627133749.png)
 - Then IntelliJ automatically create getters and setter and even value assigning part in the "Main" class.