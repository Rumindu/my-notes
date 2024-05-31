# String
- String is a ***reference type variable***, Even it declare as primitive type one.
  ```java
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
1. ***endsWith() / startWith()***
  ```java
  public class Main {
      public static void main(String[] args) {
          String message = "Hello, World!"+"!!";
          //If the message ends with "!!", return true, otherwise return false
          System.out.println(message.endsWith("!!"));
      }
  }
  ```
  - result is- `true`
  - For `startsWith()`- //If the message starts with "!!", return true, otherwise return false

2. ***length()***
  ```java
  public class Main {
      public static void main(String[] args) {
          String message = "Hello, World!"+"!!";
          //return the length of the string with the spaces
          System.out.println(message.length());
      }
  }
  ```
  - Here length of the string will include spaces
  
3. ***indexOf()***
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

4. ***replace(target,replacement)***
  ```java
  public class Main {
      public static void main(String[] args) {
          String message = "Hello, World!"+"!!";
          System.out.println(message.replace("!", "?"));
      }
  }
  ```
  - to `replace` method we need to pass 2 parameters.
	  1. target
	  2. replacement
- Difference between parameters & arguments is here target & replacement are parameters and values which are passing (! & ?) are arguments

5. toLowerCase/ toUpperCase
6. trim() - for remove spaces behind and after the string