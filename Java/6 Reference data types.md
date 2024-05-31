# Reference type
- e.g.- date object, mail message
-  apart from 8 primitive types rest of data types are reference types
```java
import java.util.Date;

public class Main {
    public static void main(String[] args) {
        byte age=30;
        //declare reference variable of Date class or
        //declare instance of Date class
        Date now = new Date();
        System.out.println(now);
    }
}
```
- Reference type doesn't holds actual value. just keep ***memory address***.
- Here is a example for referencing.
  ```java
  import java.awt.*;

  public class Main {
      public static void main(String[] args) {
          Point point1 = new Point(1, 1);
          // Declare a new variable point2 and assign point1 to it
          Point point2 = point1;
          // Change the x coordinate of point1
          point1.x = 2;
          // but the x coordinate of point2 is also changed
          System.out.println(point2);
      }
  }
  ```
  ![](assets/Pasted%20image%2020240529220042.png)
  - Here we can see point 1 and point 2 aren't independent with each other