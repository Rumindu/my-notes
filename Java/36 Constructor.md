# Constructor
- There is issue on our previous code.
- What happen if we forget to assign value to "hourlyRate" and "baseSalary" attributes after the initialize object from Employee class in the Main class.
- let get 0 for "hourlyRate" and "baseSalary".
  ``` java 
  //Main.java
  public class Main {
      public static void main(String[] args) {
          var employee = new Employee();
          // forgot those lines
  /*      employee.hourlyRate = 50;
          employee.baseSalary = 30_000;
  */
          System.out.println(employee.baseSalary); // 0
          int wage = employee.calculateWage(10);
          System.out.println(wage); //0
      }
  }
  ```

  ``` java 
  //Employee.java
  public class Employee {
      public int baseSalary;
      public int hourlyRate;
      public int calculateWage(int extraHours) {
          return baseSalary + (hourlyRate * extraHours);
      }
  }
  ```
- This is bad implementation. Because when we are using object from Employee class we need to ***follow the order*** else we get 0.
- To prevent this issue at the time we create object we can pass values to the attributes. Then we don't forget. For that we use constructor. 
- ***Constructor*** is a special method called when create new object. 
- Look at this object creation `var employee = new Employee();`. Here `Employee()` looks like calling a method.
- We have a method in this same name(Employee()) in the Employee class created by java compiler automatically. This called constructor.
- It used to create/construct new employee object from the Employee class.
- Job of this constructor initialized attributes from it's default value. It means if the attribute is a int is going to be `o`, Boolean is going to be `false`, String or reference type is going to be `null`.
``` java 
//Employee.java
public class Employee {
    private int baseSalary;
    private int hourlyRate;

    //Java compiler doesn't create default constructor
    //this is a custom constructor. But it should name as class name
    //constructor doesn't have return type not even a void
    public Employee(int baseSalary, int hourlyRate) {
        //We can use the below commented way to set the values. But there is no validation
        //this.hourlyRate = hourlyRate;
        //this.baseSalary = baseSalary;
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
    }
    
    //declared as private to simplified interface of the class
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

    public int calculateWage(int extraHours) {
        return baseSalary + (hourlyRate * extraHours);
    }
}
```

``` java 
//Main.java
public class Main {
    public static void main(String[] args) {
        //initialize the object with the constructor
        var employee = new Employee(50_000, 20);
        int wage = employee.calculateWage(10);
        System.out.println(wage);
    }
}
```