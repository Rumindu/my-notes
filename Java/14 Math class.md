# Math Class
- Use for preforming mathematical operations.
## round()
- This method is overloaded
	1. First implementation, takes `float` and returns `double`.
	2. Second implementation, takes `double` and return `long`
	![](assets/Pasted%20image%2020240609135404.png)
``` java
public class Main {
    public static void main(String[] args) {
        int result=Math.round(1.5F);
        System.out.println(result); //2
    }
}
 ```
## ceil()
- This method return `double`
  ```java 
	public class Main {
    public static void main(String[] args) {
        //ceil() is returning double value.
        //explicitly type casting to int
        int result=(int)Math.ceil(1.5F);
        System.out.println(result); //2
    }
	}
	```
## floor
``` java 
public class Main {
    public static void main(String[] args) {
        //floor() is returning double value.
        //explicitly type casting to int
        int result=(int)Math.floor(1.5F);//1
        System.out.println(result); //2
    }
}
```

## max()
- This method is overloaded
	1.  first implementation is 2 `int`s
	2. second implementation is 2 `long`s
	3. third implementation is 2 `float` s
	4. fourth implementation is 2 `double`s
	![](assets/Pasted%20image%2020240609140824.png)
	
``` java 
public class Main {
    public static void main(String[] args) {
        int result=Math.max(1,2);
        System.out.println(result); //2
    }
}
```
- Similar to this we have `min()`

## random()
- generating random values ***between 0 and 1 inclusive 0 but exclusive 1.***
- It returns `double` value
	``` java 
	public class Main {
		public static void main(String[] args) {
				double result=Math.random();
				System.out.println(result);
		}
	}
	```
	![](assets/Pasted%20image%2020240609141631.png)
	