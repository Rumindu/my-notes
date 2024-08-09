# Classes & Objects in java
- In java each class for separate file.
- Inside the `src` folder create "TextBox" class file.
  ![](assets/Pasted%20image%2020240618140257.png)
-  naming convention of class is ***Pascal Case***
- Text Box class is mentioned below
	``` java 
	//TextBox.java
	public class TextBox {
	    //define attributes
	    public String text = "";
	
	    //define methods
	    public void setText(String text) {
	        //we couldn't set value of attribute "text" like this
	        // "text=text;", Because text=text; is ambiguous because
	        // both the instance variable and the parameter have the same name.
	        // Java will assume you are referring to the parameter text,
	        // not the attribute "text".
	
	        //"this" is reference to the current object
	        //we only need to use this when parameter name is same as attribute name.
	        this.text = text;
	    }
	    public void clear() {
	        // "this" is no need to use
	        text = "";
	    }
	}
	```
- Creating object using "TextBox" class in the `Main.java`.
  ``` java
  //Main.java 
  public class Main {
      public static void main(String[] args) {
          //create an instance of TextBox
          TextBox textBox1 = new TextBox();
          //we can simplify above declaration like this.
          //Here Java compiler will automatically determine
          // the type of the variable base of right side of 
          // assignment operator.
          //This is the usual way of creating objects
          var textBox = new TextBox();
          //accessing members of TextBox class  using . operator
          textBox.setText("Text box");
          System.out.println(textBox.text);//Text box
      }
  }
  ```
- If we `System.out.println(textBox.text);` without calling `textBox.setText();` We will get `null`. Because in "TextBox" class `text` variable is just initialize as a String only. not assigning a value. then by default it will allocated null. Because string is reference type.
- These initialization can be dangerous, it can crash programs
  ``` java
  //Main.java
  public class Main {
      public static void main(String[] args) {
          TextBox textBox1 = new TextBox();
          var textBox = new TextBox();
          //try to upper case a null string
          System.out.println(textBox.text.toUpperCase());//getting null pointer exception
      }
  }
  ```
  ![](assets/Pasted%20image%2020240619104436.png)
- We can prevent this happening by initializing `String test` as empty string
  ``` java 
  public String text="";
  ```
- Showing independency of objects of same class
  ``` java 
  //Main.java
  public class Main {
      public static void main(String[] args) {
          // Create two TextBox objects
          TextBox textBox1 = new TextBox();
          textBox1.setText("Box 1");
          System.out.println(textBox1.text);
          var textBox2 = new TextBox();
          textBox2.setText("Box 2");
          System.out.println(textBox2.text);//Text box
      }
  }
  ```
  ![](assets/Pasted%20image%2020240619124406.png)