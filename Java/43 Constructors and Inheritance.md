# Constructors and Inheritance
- Generate constructor using IntelliJ IDE
	- In navigation bar `code->generate`
	- choose `constructor`
	- By default selected all parameters. If we can ignore those 
- Order of convention of the java developer use
	- 1st attributes/fields
	- then have constructor
	- finally all the public methods
- ***We don't nee to put extra effort either child class's constructor has parameters or not. But when the parent class constructor has parameters. we had to heddle it in different manner in the sub class***.
  
# No parameters in the parent class constructor
``` java 
//UIControl.java
//parent class
public class UIControl{
    private boolean isEnabled = true;

    public UIControl() {
        System.out.println("UIControl");
    }

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

``` java 
package com.rumindu;
//TextBox.java
//child class
public class TextBox extends UIControl {
    private String text = "";

    public TextBox() {
        System.out.println("TextBox");
    }

    public void setText(String text) {
        this.text = text;
    }
    public void clearText() {
        text = "";
    }
}
```

``` java 
//main.java
public class Main {
    public static void main(String[] args) {
        var box1= new TextBox();
		//1. parent constructor- UIControl
		//2. child constructor- TextBox
    }
}
```
- output
	![](assets/Pasted%20image%2020240711160150.png)
-  Here we can see parent's class constructor's S.O.P, first and child class constructor's S.O.P. 2nd.

# Parameters in the parent class constructor
- Parent class's constructor has parameters
	``` java 
	//parent class
	public class UIControl{
			private boolean isEnabled = true;

			public UIControl(boolean isEnabled) {
					this.isEnabled=isEnabled;
					System.out.println("UIControl");
			}
			...
			
	} 
	```
- Then we can see the compile error in child class.
	![](assets/Pasted%20image%2020240711162650.png)
- To get rid from this error, use `super()` to called the parent class's constructor.
- This `super()` must be placed on very first in the child class constructor.
``` java 
//TextBox.java
//child class
public class TextBox extends UIControl {
    private String text = "";

    public TextBox() {
        //must contain very first otherwise compile error.
        super(false);
        System.out.println("TextBox");
    }
		...
}
```

[GitHub](https://github.com/Rumindu/CodeWithMosh-The-Ultimate-Java-Mastery-Series/tree/constructors-and-inheritance)