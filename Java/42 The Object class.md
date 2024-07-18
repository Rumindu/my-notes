# Object Class
- Every class we declared in java, directly or indirectly inherit from the `Object` class.
- In previous example `TextBox` class inherit from the `UIControl` class and `UIControl` extends/inherit from the `Object` class. 
- We don't need to type `extends Object`. because java compiler automatically add.
  ``` java 
  //no need to add this "extends Object" part
  public class UIControl extends Object{}
  ```
- `Object` class is declared in `java.lang` package. So it's available every where
  ![](assets/Pasted%20image%2020240710225809.png)
- The `Object` class is the reason for having some additional methods apart from we declared in the class.
## Members of Object class
- getClass() 
	- returns `Class` object. From this we can read metadata of an object. Foe example we can find all attributes and methods define in object.
- equals()
	- Comparing objects
- hashCode()
	- Returns an integer base on an address on memory.
- toString()
	- Returns String representation of an object
- ...
![](assets/Pasted%20image%2020240710230601.png)

## hash Code()
``` java 
public class Main {
    public static void main(String[] args) {
        var box1= new TextBox();
        System.out.println(box1.hashCode());//250421012
    }
}
```
- We get this integer `250421012`. This is calculated base on address of in this object(`box1`) on memory.
- This isn't memory address.
- We get same hash code when referencing same object 
  ``` java 
  //Main.java
  public class Main {
      public static void main(String[] args) {
          var box1= new TextBox();
          var box2= box1;
          System.out.println(box1.hashCode());//250421012
          System.out.println(box2.hashCode());//250421012
  }
  }
  ``` 

## equals()
- This method comparing hash code of objects.
- If hash codes are equal it returns true else it returns false
- If compare above example's box1 and box2 objects using `object1Name.equals(object2Name)`. we will get result as `true`
  ``` java 
  //Main.java
  public class Main {
      public static void main(String[] args) {
          var box1= new TextBox();
          var box2= box1;
          
          System.out.println(box1.equals(box2));//true
      }
  }
  ``` 
- But is comparing 2 objects from the `TextBox` class, `equals()` returning false.
  ``` java 
  //Main.java
  public class Main {
      public static void main(String[] args) {
          var box1= new TextBox();
          var box2= new TextBox();

          System.out.println(box1.equals(box2));//false
      }
  }
  ```

## toString()
- This methods is return string representation of an object.
  ``` java 
  //main.java
  public class Main {
      public static void main(String[] args) {
          var box1= new TextBox();
          var box2= new TextBox();
          System.out.println(box1.toString());
          //com.rumindu.TextBox@eed1f14
      }
  }
  ```
  - string representation of an object has 2 parts
	  - `com.rumindu.TextBox`- fully qualified name(PackageName.ClassName) of the class. If it isn't inside the package just shoe name of the class.
	  - `@` and `hasCode value in hexadecimals`.