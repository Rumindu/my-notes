# Deep Inheritance Hierarchies
- Don't create deep inheritance hierarchies
- Inheritance is good up to 1 or 2 layers
- example for deep inheritance hierarchies
  ![](assets/SmartSelect_20240808_071519_Samsung%20Notes.jpg)
  - Problems is, classes which are involving inheritance hierarchy, are tightly couple for each others.  
  - If we make any changes on `Entity` class we have to modify `User` and `Course` classes.
	  - ex- If we change the constructor of `Entity` by adding or removing parameters we have to modify all child classes.
  - When introduce methods or attribute one of base classes But that property doesn't make sense to inherit its child classes will polluting inheritance hierarchy from irrelevant stuff. 
- Here is how to collapse above hierarchy. 
![](assets/SmartSelect_20240809_085254_Samsung%20Notes.jpg)