# Procedural Programming in java
- Here is the simple wage calculator program in procedural way.
  ``` java
  //Main.java
  public class Main {
      public static void main(String[] args) {
          int baseSalary = 50_000;
          int extraHours = 10;
          int hourlyRate = 20;
          int wage = calculateWage(baseSalary, extraHours, hourlyRate);
          System.out.println(wage);
      }
      //methods, define in Main class should be static
      //because we aren't creating an instance of Main class
      public static int calculateWage(
              int baseSalary,
              int extraHours,
              int hourlyRate
      ) {
          return baseSalary + (extraHours * hourlyRate);
      }
  }
  ```
- Even java is OOP language, this isn't object oriented programming.
- ## What are the disadvantages of this way
	1. For the bigger programs main method will be to large.
	2. Main class will be so confusing having bunch of variables and functions.
	3. Hard to maintain code.
	4. Lack of reusability.
	
- ## Symptoms of procedural programming. 
	1. Methods which have so many parameters.
	2. Constantly calling methods and passing arguments. 