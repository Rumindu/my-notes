# Hello world 
- 
  ``` jshell
  jshell> System.out.print("Hello world");
  Hello world
  ```
# Common mistakes
1. What happen if we forget to put ***close prentices***. 
    ```jshell
    jshell> System.out.print("Hello world"
   ...>
    ```
    It will look like this. so we need to put `);` to execute this statement.
    ```jshell
    jshelSystem.out.print("Hello world"
   ...> );
    Hello world
    ```

2. Forget to closing double quote. 
    ```jshell
    jshell> System.out.print("Hello world);
    |  Error:
    |  unclosed string literal
    |  System.out.print("Hello world);
    ```

3. put single quote intend of double quote
    ```jshell
    jshell> System.out.print('Hello world');
    |  Error:
    |  unclosed character literal
    |  System.out.print('Hello world');
    |
    ```
    - But in python or js we can use `"` intend of `'`