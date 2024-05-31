# Primitive Data types
- There are 2 data types
	1. Primitive data type - For storing simple values
	2. Reference data type- For storing complex objects

![](assets/Pasted%20image%2020240529151122.png)
- example
  ```java
  public class Main {
      public static void main(String[] args) {
          byte age = 30;
          // to be more readable large numbers we put "_" 
          int Subscriber = 123_456_789;
          //It is compulsory to put "L" as suffix. Else it is consider as int
          //Here if viewCount is out of range of int therefore it must be long
          long viewCount = 3_567_890_345L;
          double price = 45.34;
          //Here we need to put "f" as suffix else by default decimal values will consider as double
          float weight = 23.90F;
          char letter = 'A';
          boolean isEligible = true;
      }
  }
  ```
  