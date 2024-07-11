# Access Modifiers
## Private and Public
- Public members are accessible from the outside of class Private members not..
- Private members aren't inherited in child classes.
- We use private members to hide the implementation details of the class. So we can change the implementation
## Protected
- Protected means public inside the same package.
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
