# Consolidating State Logic with a Reducer

1. **Explanation of existing `<Counter>`**
    ``` tsx 
    const Counter = () => {
      // state variable for storing count
      const [value, setValue] = useState(0);

      return (
        // 2 button for increase and reset the value 
        <div>
          Counter ({value})
          <button
            onClick={() => setValue(value + 1)}
          >
            Increment
          </button>
          <button
            onClick={() => setValue(0)}
          >
            Reset
          </button>
        </div>
      );
    };
    ```
    [source code](https://github.com/Rumindu/codeWithMosh-react-course-part2/blob/915fb8faa5b1750b9838f919cfb658bb3c3233e7/src/state-management/Counter.tsx)
    
    ![](assets/Pasted%20image%2020250114074452.png)

2. **Why we need a reducer** 
   - When program is getting grow, keeping track of how state get updated be little bit challenging. So then we use reducer
   - Using Reducer we can take all the state management logic outside of `<Counter>` component and centralized it inside the single function. 
   
3. **Create a Reducer Function**  
   - The reducer function takes 2 parameters: 
     1. `state`: the current state.
     2. `action`: an object describing what is the user trying to do.
   - Reducer takes current state and action and returns a new state
    ``` ts 
    // reducers/counterReducer.ts
    interface Action {
      // we can add string instead of union. but this approach is more type safe
      type: "INCREMENT" | "RESET";
    }

    export function counterReducer(state: number, action: Action): number {
      if (action.type === "INCREMENT")
        return state + 1;
      if (action.type === "RESET")
        return 0;
      return state;
    }
    ```
    [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part2/blob/5c3b25b0584b95bfaabd37379e06556657c72c14/src/state-management/reducers/counterReducer.ts)

4. **Use the `useReducer` Hook in the Component**  
  
    ``` tsx 
    //Counter.tsx
    import { counterReducer } from "./reducers/counterReducer";

    const Counter = () => {
      //now we replace the useState with useReducer
      // const [value, setValue] = useState(0);
      const [value, dispatch] = useReducer(counterReducer, 0);
      return (
        //
        <div>
          Counter ({value})
          <button
            onClick={() => dispatch({ type: "INCREMENT" })}
          >
            Increment
          </button>
          <button onClick={() => dispatch({type:"RESET"})} >
            Reset
          </button>
        </div>
      );
    };
    ```
    [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part2/blob/5c3b25b0584b95bfaabd37379e06556657c72c14/src/state-management/Counter.tsx)

   - Use the `dispatch` function to send actions to the reducer. Actions are objects containing a `type` property with a specific value (e.g., `"INCREMENT"` or `"RESET"`).

5. **TypeScript Enhancements**
    
   - Define a **union type** for the `type` property to ensure only valid actions are allowed.
   - TypeScript will catch errors when invalid actions are dispatched.
    ``` tsx
    // counterReducer.ts
    export interface Action {
      type: "INCREMENT" | "RESET";
    }
    ```


6. **Benefits of Using Reducers**

   - Centralized state logic.
   - Better separation of concerns: Components focus on rendering; reducers handle state changes.
   - Reusability: Reducers can be shared across components with similar state management needs.
   - Type safety: TypeScript ensures that only valid actions and state updates are allowed.