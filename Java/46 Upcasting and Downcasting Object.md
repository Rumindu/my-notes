# Upcasting and Downcasting
 
| Upcasting                                    | Downcasting                                |
| -------------------------------------------- | ------------------------------------------ |
| Casting an object to one of its parent types | Casting an object to one of its child type |
- decaling a method called `show` to called `toString()` methods of `UIControl` class
  ``` java 
  //main.java
  public class Main {
      public static void main(String[] args) {
          var control = new UIControl(true);
          show(control);
      }
      //passing UIControl object as a parameter.
      public static void show(UIControl control){
          //call toString() method of UIControl class
          System.out.println(control);//com.rumindu.UIControl@1b28cdfa
      }
  }
  ```

  ``` java 
  //UIControl.java
  public class UIControl{
      private boolean isEnabled = true;

      public UIControl(boolean isEnabled) {
          this.isEnabled=isEnabled;
      }
      ...
  }
  ```

## Upcasting
- What if pass `textBox` object which is an instance of `TextBox` class(`UiControl` class's child class) passed to `show` method.
``` java 
//main.java
public class Main {
    public static void main(String[] args) {
        var control = new UIControl(true);
        var textBox = new TextBox();
        show(textBox);
    }

    public static void show(UIControl control){
        System.out.println(control);//com.rumindu.TextBox@eed1f14
    }
}
```
- This code is perfectly valid because `textBox` object inherit all of the members of the `control` object. Therefore ***every textBox object is a control object***.
- That is why we say inheritance represent ***is a*** relationship. A textBox is a control.
- We passed the `textBox` object into `show()` method and passed object automatically caste to `UIControl`.
- This called upCasting.
  ``` java 
  //Main.java
  public class Main {
      public static void main(String[] args) {
          var control = new UIControl(true);
          var textBox = new TextBox();
          //passing textBox object.
          show(textBox);
      }
      //casting TextBox class textBox object to UIControl class type object
      //this is called upcasting
      public static void show(UIControl control){
          //call toString() method of UIControl class
          System.out.println(control);//com.rumindu.UIControl@1b28cdfa
      }
  }
  ```
- We can also change parameter type `UIControl` to `Object`. Because every `TextBox` is also `Object`
  ``` java
  //Main.java 
  ...
  public static void show(Object control){...}
  ...
  ```
- When the Main.java file executed, nothing is console logging. Because previous lesson we override default behavior of `toString()` method at `TextBox` class.

## Downcasting
- At run time we access intense `TextBox`. But in compile time we couldn't access `TextBox`. It means if we type `control.` we can only see members of `Control` class. we can't see members of `TextBox class`
  ![](assets/Pasted%20image%2020240714151250.png)
- When we need to work with methods of `TextBox` class we need to ***downcast*** control object in to `TextBox` type. Now we can see the members of `TextBox`class.
 ![](assets/Pasted%20image%2020240714152752.png)
``` java 
//Main.java
public class Main {
    public static void main(String[] args) {
        var control = new UIControl(true);
        var textBox = new TextBox();
        show(textBox);
    }
    public static void show(UIControl control){
        //downcasting
        var textBox = (TextBox)control;
        textBox.setText("Hello World");

        System.out.println(control);//output: "Hello World"
    }
}
```
- ***Quick Recap***-
	 Because `show()` method accept `UIControl` type object or any of its [derivatives](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/object-oriented/inheritance)(ex-`Object` class). At compile time we can only access members of the `UIControl`. Unless we explicitly cast this object in to different type. That is called ***Downcasting***.
 
## Problem of above implementation and solution.
- If we pass `control` object to `show()` method. There will be an exception
  ![](assets/Pasted%20image%2020240714154923.png)
  error is `Exception in thread "main" java.lang.ClassCastException: class com.rumindu.UIControl cannot be cast to class com.rumindu.TextBox (com.rumindu.UIControl and com.rumindu.TextBox are in unnamed module of loader 'app')`
- Here is the reason for above error
	 - through this line `var textBox = (TextBox)control;` we try to cast `Control` to `TextBox`. Every `textbox` is a `control` object. But not every `control` object isn't `textBox`. It may be `checkBox, dropDownList,...`
	 - When casting generic type to specialist type we should be aware more.
- From below way we can prevent occurring above exception
    ``` java 
    //Main.java
    public static void show(Object control){
            //insteanceof operator return true if the object is an instance of the specified type
            if(control instanceof TextBox){
                var textBox = (TextBox)control;
                textBox.setText("Hello World");
            }
            System.out.println(control);
        }
    ```
	 
[Github](https://github.com/Rumindu/CodeWithMosh-The-Ultimate-Java-Mastery-Series/tree/object-upcasting-and-downcasting)