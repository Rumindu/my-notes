# Static fields/attributes & methods
- In OOP class has 2 members.
	- Instance members
	- Static members
- Instance members belongs to the instance of an object.
- ex-
	``` java 
	//Employee.java
	public class Employee {
			//Instance fields/attributes
			private int baseSalary;
			private int hourlyRate;

			//Instance methods
			public Employee(int baseSalary, int hourlyRate) {
					setBaseSalary(baseSalary);
					setHourlyRate(hourlyRate);
			}
			public Employee(int baseSalary) {
					//calling first constructor
					this(baseSalary, 0);
			}
			public int calculateWage(int extraHours) {
					return baseSalary + (hourlyRate * extraHours);
			}
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
- When we create an employee and can access these members using "objectName" with `.` operator.
  ![](assets/Screenshot%202024-07-05%20103023.png)

## Static or class members.
- Static members are belongs to a class. not an object.
- We can access those using "ClassName" with `.` operator.
	![](assets/Pasted%20image%2020240705110921.png)
	
## When do we use static members 
- When the concept that should be in single place.
- Ex- 
	Employee count-`Employee.numberOfEmployees` this concept doesn't belongs to each individuals of the employee. 

## Static fields/attributes

- We use static fields/attributes when the value is independent from the object and share across all object.
``` java 
//Employee.java
public class Employee {
	private int baseSalary;
	private int hourlyRate;
    
    //static field
    public static int numberOfEmployees;
    
    public Employee(int baseSalary, int hourlyRate) {
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
        //Once an object is created, the constructor is called
        // and the numberOfEmployees is incremented
        numberOfEmployees++;
    }
	...
}
```

``` java 
//Main.java
public class Main {
    public static void main(String[] args) {
	    //here instantiate the object due to increase the number of employees
        var employee1=new Employee(5000);
        //accessing static variable
        System.out.println(Employee.numberOfEmployees);//1
    }
}
```
 
## Static methods
``` java 
//Employee.java
public class Employee {

    private int baseSalary;
    private int hourlyRate;
    public static int numberOfEmployees;
    public Employee(int baseSalary, int hourlyRate) {
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
        //Once an object is created, the constructor is called
        // and the numberOfEmployees is incremented
        numberOfEmployees++;
    }
    //static function
    public static void printNumberOfEmployees() {
        System.out.println(numberOfEmployees);
    }
	...
}
```

``` java 
//Main.java
public class Main {
    public static void main(String[] args) {
        //here instantiate the object due to increase the number of employees
        var employee1=new Employee(5000);
        //calling static method
        Employee.printNumberOfEmployees();
    }
}
```

- Inside the class, ***Static methods can only see other static methods and static attributes***. can't access instance/normal methods and normal attributes.
 ![](assets/Pasted%20image%2020240705111508.png)
- To access instance methods we need to create an object. then we can access those methods using objectName with `.` operator. 
	``` java 
	public static void printNumberOfEmployees() {
					System.out.println(numberOfEmployees);
					new Employee(5000, 20).calculateWage(20);
			}
	```
-  That's why At the first part of the series all the methods in the main class declared as static methods. Because main method is also a static method.

## Why main method is declared as static method
- Because java runtime directly call the main method without create an object.
---
- Some examples for static members
	- `System.out.println();` This `System` class has many static members and `out` is one of it.