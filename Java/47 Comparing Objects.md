# Comparing Objects from overriding `equals()`
- There is a `Point` class.
  ``` java 
  //Point.java
  public class Point {
      private int x;
      private int y;

      public Point(int x, int y) {
          this.x = x;
          this.y = y;
      }
  }
  ```
- We create 2 instances from the `Point` class at the `Main` class and pass same coordinates as values 
  ``` java 
  //Main.java
  public class Main {
      public static void main(String[] args) {
          Point point1 = new Point(1, 2);
          Point point2 = new Point(1, 2);
          System.out.println(point1.equals(point2));// false
          //Can represent "point1 == point2" intend of 
          //"point1.equals(point2)"   
      }
  }
  ``` 
- In above example even both objects' coordinates are equal, but we get `false` as result. Because [equals()](42%20The%20Object%20class##equals()) comparing only hash code of 2 objects.
- So we need to Override behavior of `equals()` method to compare 2 `point` objects base of coordinates in the `Point` class.
- We can create this override method in easy way using IntelliJ code generate (`alt+insert`) option.
  ![](assets/Pasted%20image%2020240718103513.png)
  ![](assets/Pasted%20image%2020240718103718.png)
  ![](assets/Pasted%20image%2020240718103937.png)
- We need to change generated override method according to the over requirement.
  ``` java 
  //Point.java
  public class Point {
      private int x;
      private int y;

      public Point(int x, int y) {
          this.x = x;
          this.y = y;
      }

      //couldn't change parameter type Object in to Point
      //(Point obj) is ❌
      //because it will change the method signature
      @Override
      public boolean equals(Object obj) {
          //downcast Object to Point
          //must to down-casting to access x and y of obj
          var other = (Point) obj;
          return x == Other.x && y == Other.y;
      }
  }
  ```
- Now we get `true`when we comparing `point1` and `point2`.

## Problem of above implementation and solution.

- Above overriding method has a issue. Because type of parameter is `Object`. Therefore we can pass any type of object. We couldn't cast any object into the Point type object.
  ``` java 
  //Main.java
  public class Main {
      public static void main(String[] args) {
          Point point1 = new Point(1, 2);
          Point point2 = new Point(1, 2);
          //passing object of TextBox class instead of Point class's object 
          System.out.println(point1.equals(new TextBox()));// false
      }
  }
  ```
  ![](assets/Pasted%20image%2020240718133949.png)
  - error is `Exception in thread "main" java.lang.ClassCastException: class com.rumindu.TextBox cannot be cast to class com.rumindu.Point (com.rumindu.TextBox and com.rumindu.Point are in unnamed module of loader 'app')`. [More explanation](46%20Upcasting%20and%20Downcasting%20Object##Problem%20of%20above%20implementation%20and%20solution.)
- modified override method
``` java 
//Point.java
public class Point{
  ...
  @Override
    public boolean equals(Object obj) {
        //if the obj is equal to the current instance of the class
        if(this == obj)
            return true;
        if(!(obj instanceof Point))
            return false;
        var other = (Point) obj;
        return x == other.x && y == other.y;
    }
}
```

## Override `hascode()`
- As a best practice, if we over ride `equal()`, we must override `hashcode()`.
- Here ***overriding method to generate hash value base on content of object*** instead of reference/memory location of object.  
``` java 
//Point.java
import java.util.Objects;
public class Point {
    ...
    @Override
    public int hashCode() {
        //`Objects` class is imported from java.util package
        //multiple values can pass to hash() and -
        //-it returns hash value according to those
        return Objects.hash(x, y);
    }
}
```

``` java 
//Main.java
public class Main {
    public static void main(String[] args) {
        Point point1 = new Point(1, 2);
        Point point2 = new Point(1, 2);
        
        System.out.println(point1.hashCode());//994
        System.out.println(point2.hashCode());//994
    }
}
```

## Shortcut for overriding `equals()` and `hascode()`
![](assets/Pasted%20image%2020240718142422.png)

[Github](https://github.com/Rumindu/CodeWithMosh-The-Ultimate-Java-Mastery-Series/tree/comparing-objects)