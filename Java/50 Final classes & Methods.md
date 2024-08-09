# Final Classes & Methods
- Final classes can't be extends. It means final classes don't have child classes.
    ``` java 
    //CheckBox.java
    //final class
    public final class CheckBox extends UIControl{
        @Override
        public void render() {
            System.out.println("Render CheckBox");
        }
    }
    ```
    ![](assets/Pasted%20image%2020240722143842.png)
- We very rarely use final classes.
- `String` class is an example for final class.
---
- Final methods shouldn't need to declared on Class
- Final methods can't override in sub classes
    ``` java 
    //parent class
    //UIControl.java
    public abstract class UIControl{
        private boolean isEnabled = true;
        public abstract void render();
        //final method
        public final void enable(){
            isEnabled = true;
        }
        public void disable(){
        isEnabled= false;
        }
        public boolean isEnabled(){
            return isEnabled;
        }
    }
    ```
- Here we can't see `enable()` in the override menu.
    ![](assets/Pasted%20image%2020240722150611.png)
[Github](https://github.com/Rumindu/CodeWithMosh-The-Ultimate-Java-Mastery-Series/tree/final-classes-%26-methods)