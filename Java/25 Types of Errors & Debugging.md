# Errors
- 2 types of errors
	1. Compile time errors - due to wrong syntax
	2. run time errors - use debugger to find those

# Debugger
- Want to print "start",0 to 4 numbers and "Finish" from below code but printing only  "start",0,2,4,"Finish". Let's debug this
	``` java 
	public class Main {
		public static void main(String[] args) {
			System.out.println("start");
			printNumbers(4);
			System.out.println("Finish");
		}
		public static void printNumbers(int limit) {
					for(int i=0;i<=limit;i+=2){
						System.out.println(i);
				}
		}
	}
	```
- We need to add a break point
## Break point
- When run the code on debugger **(Debug Main)** , code will execute up until to the break point line (Line which belongs to breakpoint doesn't execute) and hold the program.   
- There are several way to add a break point
	1. just click on the relevant line number
	2. point curser on the relevant line and go to `Run -> Toggle Breakpoint -> Line Breakpoint` or use `ctl + f8` shortcut
	![](assets/Pasted%20image%2020240616141616.png)

## Debugging
- After add a break point we can click on `Debug Main`.java icon.
  ![](assets/Pasted%20image%2020240616135948.png)
- Or `Run -> Debug Main.java`  
- Then we can see debug menu
	![](assets/Pasted%20image%2020240616140304.png)
- To ***execute next line*** we need to click on `step over` icon on debugger menu 
  ![](assets/Pasted%20image%2020240616140534.png)
- Then if we go to `console` tab in debugger menu we can see "start" is printed and next line is highlighted on code editor.
	![](assets/Pasted%20image%2020240616141704.png)
- Again clicked on `step over` then line 5 will executed and we can see 2 and 4 is printed on console. Then we identify bug is on `printNumber()` method
	![](assets/Pasted%20image%2020240616141726.png)
- Now we need to investigate  `printNumber()` method. but now we are on 6th line. So we need to rerun the program and ***step in*** to this method. For rerun the program we need to click on "rerun" button.
  ![](assets/Pasted%20image%2020240616143907.png)
- Once we are on line 5 we need to clicked on "step into" button
  ![](assets/Pasted%20image%2020240616144120.png)
- Once we step in to we can see the bug on for loop's increment operation.
  ![](assets/Pasted%20image%2020240616144323.png)
- We can iterate this loop using "step over" button. Here we complete first iteration of loop.
	![](assets/Pasted%20image%2020240616144552.png)
- Add debugger panel we can see "variable window" and it automatically detected variables of current scope and show.
  ![](assets/Pasted%20image%2020240616144805.png)
- We can also manually add variable to watch its value from `right click on debugger pannel -> + New watch -> insert varaible name`
  ![](assets/Pasted%20image%2020240616145016.png)
- When the variable doesn't need any more we can delete it using right click on relevant watch variable.  
	![](assets/Pasted%20image%2020240616145154.png)
- Identify the bug and resolve the increment operation. Once we change the code we need to rerun program using "Rerun" button
	![](assets/Pasted%20image%2020240616143907.png)
- To check whether bug is solved remove break point of main method and add a break point in for loop. Once Clicked on "Resume program" button we can continue execute up to the next break point. In here line 9
  ![](assets/Pasted%20image%2020240616145914.png)
- Next time when we restart debugging it is start on line 9.
- We can setup out from the method even it isn't fully executed using "step out" button. 
  ![](assets/Pasted%20image%2020240616150339.png)
- In the frame method we can see all called methods in the reverse order
  ![](assets/Pasted%20image%2020240616150548.png)