# Method Overloading
- ***Same method name*** but they have ***different parameters*** due to different implementation.
- Assume when an employee doesn't work extra hours. We can either pass `0` or create a different implementation of same method that doesn't take any parameters.
  ``` java 
  //Main.java
  public class Main {
      public static void main(String[] args) {
          var employee = new Employee(50_000, 20);
          //we can overload the method calculateWage either by passing 
          // the extraHours or without passing any parameter
          int wage = employee.calculateWage(10);
          int wage1 = employee.calculateWage();
      }
  }
  ```
Can achieve method overloading in the "Employee.java" file in 2 ways
- 1st way
  ``` java 
  //Employee.java
  public class Employee {
      private int baseSalary;
      private int hourlyRate;

      public Employee(int baseSalary, int hourlyRate) {
          setBaseSalary(baseSalary);
          setHourlyRate(hourlyRate);
      }
      //overloading the method calculateWage
      public int calculateWage(int extraHours) {
          return baseSalary + (hourlyRate * extraHours);
      }
      public int calculateWage() {
          return baseSalary ;
      }

      private void setBaseSalary(int baseSalary) {
          if (baseSalary <= 0)
              throw new IllegalArgumentException("Salary cannot be 0 or less");
          this.baseSalary = baseSalary;
      }
      private void setHourlyRate(int hourlyRate) {
          if (hourlyRate < 0)
              throw new IllegalArgumentException("Hourly rate cannot be 0 or less");
          this.hourlyRate = hourlyRate;
      }
  }
  ```
- 2nd way- call the first method inside the second method
  ``` java 
  //Employee.java
  public class Employee {
      private int baseSalary;
      private int hourlyRate;

      public Employee(int baseSalary, int hourlyRate) {
          setBaseSalary(baseSalary);
          setHourlyRate(hourlyRate);
      }
      //overloading the method calculateWage
      public int calculateWage(int extraHours) {
          return baseSalary + (hourlyRate * extraHours);
      }
      //changed part
      public int calculateWage() {
          return calculateWage(0) ;
      }

      private void setBaseSalary(int baseSalary) {
          if (baseSalary <= 0)
              throw new IllegalArgumentException("Salary cannot be 0 or less");
          this.baseSalary = baseSalary;
      }
      private void setHourlyRate(int hourlyRate) {
          if (hourlyRate < 0)
              throw new IllegalArgumentException("Hourly rate cannot be 0 or less");
          this.hourlyRate = hourlyRate;
      }
  }
  ```
- Overloading method is to many times made application hard to maintain.