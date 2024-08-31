# Interface
- Most miss understood feature in java Because meaning of interface change since java 8
- We use interface for loosely coupled, extensible, testable application.
- coupling - Level of depending two software entities like classes. 
  ![](assets/SmartSelect_20240809_142829_Samsung%20Notes.jpg)
- With Interfaces we can completely decoupled classes.
  ![](assets/SmartSelect_20240809_143537_Samsung%20Notes.jpg)
- Interfaces are similar to classes But it only contain method declaration. No implementation
  ![](assets/Pasted%20image%2020240809142940.png)
  

  | Interface                                                    | Classes            |
  | ------------------------------------------------------------ | ------------------ |
  | What should be done<br>ex- <br>Data compression<br>Searching | How should be done |
- ex- Building an application for calculating taxes. Each year tax rules might change, but every year you need to able to calculate tax. So interface specifies what should be done, which is calculating taxes and different classes will provide different ways for calculating tax each year. So we can swap one implementation with another.