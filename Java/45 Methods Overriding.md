# Overriding methods
- Override/change methods which inherited from the parent class in child class.
- ex- Every object has `toString()` method which is inherited from `object` class which returns `packageName.ClassName@hexadecimalValueOfhashCode()value`. But we need to this methods behavior. Once we call it we need to return the value of `text` property in `TextBox` class
  ``` java 
  //main.java
  public class Main {
      public static void main(String[] args) {
          var textBox=new TextBox();
          //toString() method in default behaviour
          System.out.println(textBox.toString());//com.rumindu.TextBox@eed1f14
      }
  }
  ```
- Use `@Override` annotation for overriding method. Annotation is a label that attached to class member which gives extra information to the java compiler.
- The overriding method must have the same return type
  ``` java 
  //TextBox.java
  public class TextBox extends UIControl {
      private String text = "";

      public TextBox() {
          super(false);
          System.out.println("TextBox");
      }
      //Overriding toString() methods that declared in Object class.
      //Object class is great parent class of TextBox class
      @Override
      public String toString(){
      return text;
      }

      public void setText(String text) {
          this.text = text;
      }
      public void clearText() {
          text = "";
      }
  }
  ``` 

- **Extra fact- 
	If the just object name is inside the `System.Out.Print()` method, By default it calls `toString()` methods in the relevant object. Therefore here we specifically no need to call `toString()` inside the `System.out.println()`
``` java 
//main.java
public class Main {
    public static void main(String[] args) {
        var textBox=new TextBox();
        //override toString() method
        System.out.println(textBox);//TextBox
        //no need to explicitly call toString()
        //System.out.println(textBox.toString());
    }
}
```
[GitHub](https://github.com/Rumindu/CodeWithMosh-The-Ultimate-Java-Mastery-Series/tree/overridding-methods)