# Arithmetic expression
## Addition, subtraction & Multiplication
``` java 
public class Main {
    public static void main(String[] args) {
        int r1= 10+5;
        int r2=10-5;
        int r3=10*5;
        // this is the way print more variables in single system.out.print()
        System.out.println(r1+" "+r2+" "+r3);
    }
}
```
![](assets/Pasted%20image%2020240608155738.png)
## Division

- In java division of 2 [whole](whole%20numbers.md) numbers is a whole number.
  ```java
  public class Main {
    public static void main(String[] args) {
        int result =10/3;
        System.out.println(result);
    }
  }
  ```
  ![](assets/Pasted%20image%2020240608173813.png)
  - Here result should be 3.3333, but we'll get 2
- To prevent that issue and result as a floating point number we need to do convert these numbers in to float or double .
``` java 
public class Main {
    public static void main(String[] args) {
        //"(double)10" is casting 'int' in to 'double'
        double result =(double)10/(double)3;
        System.out.println(result);
    }
}
```