# Increment Operator(`++`)
- How to increment value of variable by 1
  ```java
    public class Main {
        public static void main(String[] args) {
            int x=1;
            //assign current value of x to the y and then increment x by 1
            int y=x++;
            //immediately increment x by 1 and then assign the value to z
            int z=++x;
            System.out.println(x);
            System.out.println(y);
            System.out.println(z);
        }
    }
    ```
- How to increment value by any number using ***augmented*** or ***compound*** assignment operator
  ```java
  public class Main {
      public static void main(String[] args) {
          int x=1;
          //x= x + 2;
          x +=2;
          System.out.println(x);
      }
  }
  ```  
- We can use subtraction, multiplication and division for above augment assignment operator by replacing relevant operator intend of plus.