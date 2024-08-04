# Loops
## For Loop
``` java 
public class Main {
    public static void main(String[] args) {
        for(int i = 0; i < 5; i++)
            //Don't need {} for only one line 
            System.out.println("Hello world");
    }
}
```
- Implementing "for loop" is cleaner comparing with other loops.
- **Better to use when iterative count is already known**

## While loop
- Let's represent above for loop from a "while loop".
``` java 
public class Main {
    public static void main(String[] args) {
        int i=0;
        //once the condition became false, the loop stops
        //or upto/until condtion is true, the loop will run
        //If u confuse refer the below example
        while (i<5){
            System.out.println("Hello World");
            i++;
        }
    }
}
```
- While loop is better to use when we don't exactly know iterate count.
  ex - ask user enter to something until type "quite" to terminate program.
  ``` java 
  import java.util.Scanner;

  public class Main {
      public static void main(String[] args) {
          String input ="";
          //don't initialize scanner object inside the loop
          //because it's create a new object each iterate.
          Scanner scanner = new Scanner(System.in);
          // we can't compare strings with == like js, we have to use the equals method
          while (!input.equals("quit")) {
              System.out.print("Enter a number: ");
              input = scanner.next().toLowerCase();
              System.out.println(input);
          }
      }
  }
  ```  

## Do-while loop
- rewrite 2nd while loop as do-while loop.
  ``` java 
  import java.util.Scanner;

  public class Main {
      public static void main(String[] args) {
          String input ="";
          Scanner scanner = new Scanner(System.in);
          do{
              System.out.print("Enter a number: ");
              input = scanner.next().toLowerCase();
              System.out.println(input);
          }
          while (!input.equals("quit"));

      }
  }
  ```
  - Do-while loops are vary rarely use.

## `Break` statement
- When the java see `Break`, it will ignore every thing after `braeak` inside the loop and terminate the loop.
``` java 
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        String input ="";
        Scanner scanner = new Scanner(System.in);
        while (!input.equals("quit")) {
            System.out.print("Enter a number: ");
            input = scanner.next().toLowerCase();
            if (input.equals("quit"))
                break;
            //due to break statement, when "quit" is entered it won't print.
            System.out.println(input);
        }
    }
}
```

## `Continou` statement
- It moves control to the beginning of the loop.
``` java 
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        String input ="";
        Scanner scanner = new Scanner(System.in);
        while (!input.equals("quit")) {
            System.out.print("Enter a number: ");
            input = scanner.next().toLowerCase();
            if (input.equals("pass")) {
                //continue will skip the rest of the loop, 
                // and go back to the beginning
                continue;
            }
            if (input.equals("quit"))
                break;
            System.out.println(input);
        }
    }
}
```
---
- Simplified the above code
``` java 
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        String input ="";
        Scanner scanner = new Scanner(System.in);
        //In this way we must include break statement.
        //otherwise it will be an infinite loop
        while (true) {
            System.out.print("Enter a number: ");
            input = scanner.next().toLowerCase();
            if (input.equals("pass")) {
                continue;
            }
            if (input.equals("quit"))
                break;
            System.out.println(input);
        }
    }
}
```
## For each loop
- use `for each` loops for iterate over array or collections.
``` java 
public class Main {
    public static void main(String[] args) {
        String [] fruits = {"Apple", "Banana", "Orange"};
        //for each loop
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
        //for loop
        for (int i = 0; i < fruits.length; i++) {
            System.out.println(fruits[i]);
        }
    }
}
```
- Limitation of for each loop
	1.  iterate array only forward way. can't print "Orange, Banana, Apple" order
	2. don't have access to index of each item