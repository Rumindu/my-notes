# Polymorphism
- It means "many forms". Which allows object to be in different shapes.
- Crate an array of control objects in `Main.java`.
    ``` java
    //In this array we can have instance of UIControl or any of its sub classes
    UIControl[] controls = {new TextBox(), new CheckBox()};
    ```
- If we want to render each controls object, it will end like this
    ``` java 
    public static void main(String[] args) {
            //array of controls
            //particle scenario is rendering a form with multiple UI Control components
            // (ex-few TextBoxes and CheckBoxes in a form
            UIControl[] controls = {new TextBox(), new CheckBox()};
            //procedural approach of call rendering different controls objects
            /*for (var control : controls) {
                if control is TextBox
                renderTextBox()
                else if control is CheckBox
                renderCheckBox()
            }*/
    }
    ```
- for get polymorphism approach above case, first we declare a `render()` method on `UIControl` class and then it override on `TextBox` & `CheckBox` classes according to relevant tasks.
    ``` java 
    //parent class
    //UIControl.java
    public class UIControl{
        ...
        public void render(){
            //this method doesn't have any implementation.
            //Implementation depends on type of object(checkBox, textBox, etc
        }
        ...
    }
    ```

    ``` java 
    //child class
    //TextBox.java
    public class TextBox extends UIControl {
        
        @Override
        public void render() {
            System.out.println("Render TextBox");
        }
    }
    ```

    ``` java 
    //child class
    //CheckBox.java
    public class CheckBox extends UIControl{
        
        @Override
        public void render() {
            System.out.println("Render CheckBox");
        }
    }
    ```
- Now every class has own render() method
- Now iterate `controls[]` and in each iteration called render method. Here control object is taking many different forms/shapes. That is called polymorphism. 
    ``` java 
    //Main.java
    public class Main {
        public static void main(String[] args) {
        
            UIControl[] controls = {new TextBox(), new CheckBox()};
            
            //Implementing polymorphism for rendering controls object
            //Here, a control object is taking many different shapes according to the array elements
            for (var control : controls) {
                control.render();
            }
        }
    }
    ```
    [Github](https://github.com/Rumindu/CodeWithMosh-The-Ultimate-Java-Mastery-Series/tree/polymorphism)