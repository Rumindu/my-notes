# Constructor Overloading
- We can overload constructor because constructor is also a method.
- Ex- Some people have base salary and extra hour salary and some only have base salary. To achieve this one way is pass 0 as `hourlyRate` to constructor and other way is overload Constructor.
	``` java 
	//Main.java
	public class Main {
			public static void main(String[] args) {
					//constructor overloading
					//employee who has no extra hours salary.
					var employee1=new Employee(5000);
					//employee who has hours salary.
					var employee = new Employee(50_000, 20);
			}
	}	
	```

Can achieve Constructor overloading in the "Employee.java" file in 2 ways.
- 1st way
``` java 
//Employee.java
public class Employee {
    private int baseSalary;
    private int hourlyRate;

    //Constructor overloading
    public Employee(int baseSalary, int hourlyRate) {
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
    }
    public Employee(int baseSalary) {
        setBaseSalary(baseSalary);
        setHourlyRate(0);
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
- 2nd way- In the 2nd constructor calling 1st constructor with passing `0` to `hourlyRate`.
``` java 
//Employee.java
public class Employee {
    private int baseSalary;
    private int hourlyRate;

    //Constructor overloading
    public Employee(int baseSalary, int hourlyRate) {
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
    }
    public Employee(int baseSalary) {
        //calling first constructor
        this(baseSalary, 0);
    } 
    ...

}
```
- #IntelliJ `ctrl + p` to get parameter info of a method.
  ![](assets/Screenshot%202024-07-05%20084150.png)