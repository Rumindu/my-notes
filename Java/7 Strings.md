# String
- String is a ***reference type variable***, Even it declare like primitive type one.
  ```java
  //String's 'S' is capital in other data types begin from simple
  String message = "Hello, World!";
  ```
- We can concatenate or join string with another string using `+`
  ```java
  String message = "Hello, World!" + "!!";
  ```
- String is a class so we can access it's methods using `.` operator.
![](assets/Pasted%20image%2020240530191225.png)
## Some methods of String class

- From these methods original `message` string isn't change. Because in Java strings are immutable. It means once it declares, we couldn't change it's value.
- ### ***endsWith() / startWith()***
  ```java
  public class Main {
      public static void main(String[] args) {
          String message = "Hello, World!"+"!!";
          //If the message ends with "!!", return true, otherwise return false
          System.out.println(message.endsWith("!!")); // true
      }
  }
  ```
  - For `startsWith()`- //If the message starts with "!!", return true, otherwise return false

- ### ***length()***
  ```java
  public class Main {
      public static void main(String[] args) {
          String message = "Hello, World!"+"!!";
          //return the length of the string with the spaces
          System.out.println(message.length());//15
      }
  }
  ```
  - Here length of the string will include spaces
  
- ### ***indexOf()***
  ```java
  public class Main {
      public static void main(String[] args) {
          String message = "Hello, World!"+"!!";
          //If the string is found, the indexOf method returns the index of the first occurrence of the specified substring.
          System.out.println(message.indexOf("Wo"));
          //If the string is not found, the indexOf method returns -1.
          System.out.println(message.indexOf("q"));
      }
  }
  ```
  ![](assets/Pasted%20image%2020240531194139.png)

- ### ***replace(target,replacement)***
  ```java
  public class Main {
      public static void main(String[] args) {
          String message = "Hello, World!"+"!!";
          //from replace(), create new string which is replaced ! by ?
          System.out.println(message.replace("!", "?"));
      }
  }
  ```
  - to `replace` method we need to pass 2 parameters.
	  1. target
	  2. replacement
  - Difference between parameters & arguments is here "target" & "replacement" are parameters and values which are passing (! & ?) are arguments

- ### ***toLowerCase() / toUpperCase()***
  ``` java 
  public class Main {
      public static void main(String[] args) {
          String message = "Hello, World!"+"!!";
          System.out.println(message.toLowerCase());//hello, world!!
      }
  }
  ```

- ### ***trim()*** - 
  - for remove spaces **behind and after** the string
  ``` java 
  public class Main {
      public static void main(String[] args) {
          String message = "  Hello, World!"+"!!  ";
          System.out.println(message.trim());//Hello, World!!!
          System.out.println(message);// Hello, World!!!
      }
  }
  ```
  - Difference between after trim and before trim
    ![](assets/Pasted%20image%2020240610101353.png)