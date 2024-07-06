# Encapsulation
- Bundle the data and methods that operate on the data inside a single object.
- We will apply encapsulation on previous lesson's code. 
- Here we bundle attributes and "calculateWage" method in to the "Employee" class 
- Add a "Employee" class.
  ``` java 
  //Employee.java
  public class Employee {
      public int baseSalary;
      public int hourlyRate;

      //Here we don't need to use "static"
      //We don't need to pass the parameters to the method
      // like previously done
      //Fewer parameters are passing to method is sign of OOP.
      //Assume extraHours will be varied for each month
      public int calculateWage(int extraHours) {
          return baseSalary + (hourlyRate * extraHours);
      }
  }
  ```
  
  ``` java 
    //Main.java
    public class Main {
        public static void main(String[] args) {
            var employee = new Employee();
            employee.baseSalary = 50_000;
            employee.hourlyRate = 20;

            int wage = employee.calculateWage(10);
            System.out.println(wage);
        }
    }
  ```