# Casting
## Implicit Casting

- Implicit casting means automatic conversion.
  ``` java 
  public class Main {
      public static void main(String[] args) {
          //Implicit casting / automatic type conversion
          short x =1;
          int y=x+2;
          System.out.println(y);
      }
  }
  ```
-  Here compiler create anonymous `int` variable to store `short x` value as integer value. then addition happen with anonymous variable and 2. 
- **This automatic conversion occurs when the converting data type’s range is less than or equal to the converted data type’s range.** Implicit casting will happen when a `short` is converted to an `int`, but not when an `int` is converted to a `short`.
- Implicit casting happens when no chance to data loss.
- byte -> short -> int -> long -> float -> double
``` java
public class Main {
    public static void main(String[] args) {
        double x =1.1;
        double y=x+2; // 1.1 + 2.0 = 3.1 
        System.out.println(y);
    }
}
```

## Explicit casting
``` java 
public class Main {
    public static void main(String[] args) {
        double x =1.7;
        int y=(int)x+2; // 1 + 2
        System.out.println(y); //3
    }
}
```
- Here we are forcely casting `double x` to `int` then `x` value became 1.
- `(int)x`, Here value of `x` is not rounding. just removing fraction values.
- We can only do this explicit casting for compatible data types. It means we can't casting `String -> int` in this method

## Casting using wrapper class
- To cast `String` in to `int` we use wrapper class of primitive data type.
  ``` java 
  public class Main {
      public static void main(String[] args) {
          String x ="1";
          //"Integer" is the wrapper class of "int"
          int y=Integer.parseInt(x)+2; // 1 + 2
          System.out.println(y); //3
      }
  }
  ```
- If we try to convert floating string using `parseInt()` we will get an exception.
- `string floating number` is convert in to the `double`
  ``` java 
  public class Main {
      public static void main(String[] args) {
          String x ="1.5";
          double y=Double.parseDouble(x)+2; // 1.5 + 2.0
          System.out.println(y); //3.5
      }
  }
  ```