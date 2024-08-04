# Inheritance
- Assume we need to create a frame work for building graphical user interface
- It can create forms with various types of
	- input fields
	- textboxes
	- check boxes
	- ....
- All of this object shares some common behaviors
	- ex-
		- enable or disable
		- size in terms of width and height
- When we code these classes, we don't need to implement all these features for every single class.
- We can use ***Inheritance*** for reuse the code.
- Define all the common behavior in single class called UI controlled and have other classes like TextBox, CheckBox,.... inherit those behavior from the UI control class 
	![](assets/Pasted%20image%2020240710094403.png)
- Parent class
	``` java 
	//UIControl.java
	public class UIControl {
			private boolean isEnabled = true;

			public void enable(){
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
- Child class
``` java 
//TextBox.java

//using "extends" key word to inherit "UIControl" class
public class TextBox extends UIControl {
    private String text = "";

    public void setText(String text) {
        this.text = text;
    }
    public void clearText() {
        text = "";
    }
}
```
- When we implementing `TextBox` class we can see `UIContainer` class's properties on `TextBox` class.
	![](assets/Pasted%20image%2020240710101734.png)
	- We can see bunch of other methods like `hashCode()...` apart from `UIContainer`'s methods. These are inherited from another class in java called `Object` class