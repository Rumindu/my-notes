# Access Modifiers
## Private and Public
- Public members are accessible from the outside of class Private members are not..
- Private members aren't inherited in child classes.
- We use private members to hide the implementation details of the class. So we can change the implementation
## Protected
- According to Mosh, using `protected` is a bad practice.
- Protected means public inside the same package.
- ***Protected members are accessible any class within the same package. But not in different packages***
- Here both `Main` class and `UIControl` inside `com.rumindu` package
  ``` java 
  //main.java
  package com.rumindu;

  public class Main {
      public static void main(String[] args) {
          System.out.println(new UIControl(true).isEnabled);//true
      }
  }
  ```

  ``` java 
  //UIControl.java
  package com.rumindu;

  public class UIControl{
      protected boolean isEnabled = true;

      public UIControl(boolean isEnabled) {
          this.isEnabled=isEnabled;
          System.out.println("UIControl");
      }
      ...
  }
  ```
- We will get a compilation error when accessing protected members of `UIControl` class from the `Main` class, if `Main` class and `UIControl` class are in separate packages
  ``` java 
  //main.java
  package com.codewithrumindu;
  //If the class is from the different package, we need to import it
  import com.rumindu.UIControl;

  public class Main {
      public static void main(String[] args) {
          System.out.println(new UIControl(true).isEnabled);
      }
  }
  ```
  ![](assets/Pasted%20image%2020240712074300.png)
- But ***Protected members are accessible in child class through different packages*** 

## Default access modifier
- If we don't provide any specific access modifier(public, private, protected)  then the property will get default access modifier.
- Members which has ***default access modifier, are public anywhere in the same package but private outside the package***.
- Even default members ***aren't accessible*** in child class through different packages.
``` java 
    //default access modifier.
    //Don't provide any access modifier prefix
    boolean isEnabled = true;
``` 
[GitHub](https://github.com/Rumindu/CodeWithMosh-The-Ultimate-Java-Mastery-Series/tree/Access-Modifers-inheritance)
