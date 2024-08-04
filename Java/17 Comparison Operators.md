# Comparison Operators
- Use for compare primitive values.
- #expression is a peace of code that produce a value.
- Here those comparison operators(`==, !=, >, <, >=, <= `) are Boolean expressions because they are only producing true or false.
``` java 
public class Main {
    public static void main(String[] args) {
       int x = 1;
       int y =1;
        System.out.println(x == y);//true
        System.out.println(x != y);//false
        System.out.println(x > y);//false
        System.out.println(x < y);//false
        System.out.println(x >= y);//true
        System.out.println(x <= y);//true
    }
}
```