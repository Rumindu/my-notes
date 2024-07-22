# Abstract Classes & Methods
- Declared class but doesn't create instance/object from this class.
    ``` java
    //Main.java
    public class Main {
        public static void main(String[] args) {
            //Couldn't create an object from an abstract class
            //var UI = new UIControl;
            UIControl[] controls = {new TextBox(), new CheckBox()};
            ...
        }
    }
    ```
- Purpose of abstract class is provide some common code to its sub classes.
- Abstract method should declared inside the abstract class.
- Abstract method doesn't contain a body.
    ``` java 
    //parent class
    //UIControl.java
    public abstract class UIControl{
        ...

        //abstract method doesn't contain a body
        //abstract method must be contained in an abstract class
        //abstract method must be overridden/implement in the child class
        public abstract void render();
        ...
    }
    ```
- When add abstract method on parent class, Every child class(except abstract child classes) must implement abstract method. 
    ``` java 
    //child class
    //TextBox.java
    public class TextBox extends UIControl {
        ...
        //Implementing an abstract method
        //no need to put @Override annotation. But it's a good practice to put it.
        @Override
        public void render() {
            System.out.println("Render TextBox");
        }
        ...
    }
    ```
- Abstract child class will be like this
    ``` java 
    public abstract class TextBox extends UIControl {...}
    ```

[Github](https://github.com/Rumindu/CodeWithMosh-The-Ultimate-Java-Mastery-Series/tree/abstract-classes-%26-methods)


