# User Inputs
- use `Scanner` class form `java.utill` package
- From Scanner class we create object like this `Scanner scanner1= new Scanner(System.in);`
- This object has bunch of methods to reading data and all this method start from ***"next"*** 
  ![](assets/Pasted%20image%2020240610140434.png)
``` java 
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        //use System.in to get input from the terminal
        Scanner scanner1= new Scanner(System.in);
        // assign user_input to a byte type variable
        // we must use "instantName"."relevant_method"(If userInput is a byte use "nextByte" if userInput value is number use "nextInt") to get the prompt.
        byte age= scanner1.nextByte();
        //implicitly casting byte -> String
        System.out.println("your age is "+ age);
    }
}
```
![](assets/Pasted%20image%2020240610141024.png)
- we can add some text before getting the age from user.
  ``` java
  import java.util.Scanner;

  public class Main {
      public static void main(String[] args) {
          Scanner scanner1= new Scanner(System.in);
          // using println, therefore the typingLine/cursor will be available in next line
          System.out.println("Age: ");
          byte age= scanner1.nextByte();
          System.out.println("your age is "+ age);
      }
  }
  ```
  ![](assets/Pasted%20image%2020240610142040.png)
  ``` java 
  System.out.print("Age: ");
  ```
  ![](assets/Pasted%20image%2020240610142141.png)
- When we type floating point number we get exception(error). To prevent that we need to use `nextFloat()` or `nextDouble()`.

- ## ***use `next()` or `nextLine` getting String inputs***

  | next                                         | nextLine                |
  |:---:                                        |:----------:              |
  |only return first word of string| return whole string|

  ``` java 
  import java.util.Scanner;

  public class Main {
      public static void main(String[] args) {
          Scanner scanner1= new Scanner(System.in);
          // using println, therefore the cursor will be in the next line
          System.out.print("Name: ");
          String name= scanner1.next();
          System.out.println("your name is "+ name);
      }
  }
  ```
  ![](assets/Pasted%20image%2020240610143407.png)

  ``` java 
  String name= scanner1.nextLine();
  ```
  ![](assets/Pasted%20image%2020240610143447.png)
  - Here if user enter spaces before the enter the string it also appearing
    ![](assets/Pasted%20image%2020240610144207.png)
- use trim() method for removing spacing before or after user inputs string.
``` java 
String name= scanner1.nextLine().trim();
```
![](assets/Pasted%20image%2020240610143959.png)
