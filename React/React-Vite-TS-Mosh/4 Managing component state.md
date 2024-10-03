# Understanding the State Hook in React

1. **State Updates are Asynchronous**
    
   - React updates the state asynchronously, meaning the state change does not happen immediately.
   - For example, after calling `setState`, if you log the state variable, you’ll see the old value until React finishes processing the update.
        ``` tsx 
        import { useState } from "react";

        const App = () => {
        const [isvisible, setIsVisible] = useState(false);
        const handleClick = () => {
            setIsVisible(!isvisible);
            console.log(isvisible);//false
        };
        return <button onClick={handleClick}>Show</button>;
        };

        export default App;
        ```
        
        ![](assets/Pasted%20image%2020241002153600.png)

   - This behavior improves performance by batching multiple state updates and re-rendering the component only once after the event handler completes.

2. **State is Stored Outside the Component**
    
   - The `useState` hook stores the state variables outside the component, in memory, to persist the values across re-renders.
   - If a regular local variable is used instead, its value will be reset each time the component re-renders, because local variables are removed from memory when the function completes execution.
   - React automatically cleans up state variables when the component is no longer visible on the screen.
  
3. **State Hook Must be Called at the Top Level**
    
   - Hooks, including `useState`, must be used at the top level of your components.
   - React relies on the order in which hooks are called to map state variables correctly. ==Using hooks inside loops, conditionals, or nested functions can disrupt this order and lead to errors.==
   - Therefore, always declare hooks at the top level of your component to ensure consistent behavior.

4. **How React Tracks State Variables**(Reason for Point 3 )
    
    - When you declare multiple state variables using `useState`, React is not aware of the variable names you assign them (e.g., `isVisible`, `isApproved`). These are just local identifiers inside the component function.
    - Internally, React stores state values (like Booleans, numbers, or arrays) in a data structure, most likely an array. Each state value is stored in the same order it was declared.
    - On subsequent re-renders, React uses the order of the state hooks to map values correctly to the variables in the function.
    - **For example**:
        ``` tsx 
        const [isVisible, setIsVisible] = useState(false);
        const [isApproved, setIsApproved] = useState(false);
        ```
        
      - In this case, React will store the values of `isVisible` and `isApproved` in the order they were declared, and it will always retrieve them in the same order on re-renders. This is why hooks cannot be called conditionally, as it would disrupt the order React relies on.
---

# Best Practices for Choosing State Structure in React

1. **Avoid Redundant State Variables**
    
   - Avoid declaring state variables for values that can be derived or computed from other existing state variables.
   - **Example**: Instead of creating a `fullName` state variable, calculate it from `firstName` and `lastName`:
        ``` tsx 
        const [firstName, setFirstName] = useState('');
        const [lastName, setLastName] = useState('');

        const fullName = `${firstName} ${lastName}`; // Computed value
        ```
   - You can render the full name directly in the JSX or store it in a local variable/constant within the component.
  
2. **Group Related State Variables**
    
   - If state variables are logically related, group them into an object rather than using multiple state variables.
   - **Example**: If managing personal information, group `firstName` and `lastName` into a `person` object:
        ``` tsx 
        // const[firstName,setFirstName]= useState('');
        // const[lastName,setLastName]= useState('');
        const [person, setPerson] = useState({ firstName: '', lastName: '' });
        ```

3. **Separate Unrelated State Variables**
    
   - If some state variables represent different concerns (e.g., a loading state and user data), avoid grouping them into a single object.
   - **Example**: Keep unrelated state like `isLoading` separate from a `person` object:
        ``` tsx 
        const [isLoading, setIsLoading] = useState(false);  // For tracking page loading state
        const [person, setPerson] = useState({ firstName: '', lastName: '' });  // For personal details
        ```
        
4. **Avoid Deeply Nested Structures**
    
   - Avoid deeply nested state structures as they are more difficult to update and maintain.
   - **Example of Deep Nesting** (to avoid):
        ``` tsx 
        const [person, setPerson] = useState({
        contact: { address: { street: '' } }
        });
        ```
        
   - Instead, **prefer a flat structure**:
``` tsx 
const [address, setAddress] = useState({ street: '' });
```
---

# Keeping Components Pure in React

1. **What is a Pure Function?**
    
   - A **pure function** is a function that, given the same input, always returns the same result. In other words, if you call the function multiple times with the same arguments, it should always produce the same output.
   - In contrast, an **impure function** may return different results even with the same input.
  
2. **React Components as Pure Functions**
    
   - React is designed around the concept of **purity**. It expects every component to behave like a pure function.
   - A React component should return the same JSX when given the same props (input), ensuring consistent output.
   - **Performance Benefit**: If the props of a component don’t change, React can optimize performance by skipping unnecessary re-renders.
  
3. **How to Keep Components Pure?**
    
   - **Avoid making changes during the render phase**: Ensure that any state or variables that existed before rendering are not modified during rendering. Modifying pre-existing variables during rendering makes the component impure.
   - **Example of Impurity**:
        ``` tsx 
        //Message.tsx
        let count = 0;

        const Message = () => {
        count++; // Modifying count during rendering
        return <div>Message {count}</div>;
        };

        export default Message;
        ```
        [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/a843ec064b9c1b11400986a0ce9fec0eaa608113/src)

        ![](assets/Pasted%20image%2020241003045203.png)
        
     - In this example, modifying the `count` variable in the render phase results in different output every time the component is rendered, making it **impure**.
  
4. **Allowable Changes During Rendering**
    
   - It is acceptable to **declare new variables within the render phase** and modify them. Since these variables are created each time the component is rendered, they don’t persist across renders, keeping the component pure.
   - **Example of Purity**:
        ``` tsx 
        //Message.tsx
        const Message = () => {
        let count = 0; // Declared as part of rendering
        count++;
        return <div>Message {count}</div>;
        };

        export default Message;
        ```
        [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/0d30994fb5a0e7300e168b67fd5f77b373b4c63a/src)
        
        ![](assets/Pasted%20image%2020241003050219.png)
        
     - In this case, `count` is initialized and modified within the render function, and it resets every time the component renders, making it **pure**.
---

# **Strict Mode in React**

1. **Strict Mode Overview**
    
   - **Strict Mode** is a feature in React that helps developers identify potential issues in their code during development. It doesn’t affect the production build and has no visual representation in the UI.
   - It is enabled by wrapping components inside the `<StrictMode>` component, often done by default in React applications:
        ``` tsx 
        //main.tsx
        <React.StrictMode>
            <App />
        </React.StrictMode>,
        ```

2. **Strict Mode and Impure Components**
    
    - In **development mode**, React renders components **twice** when Strict Mode is enabled, but only takes the result of the second render. This double rendering helps detect side effects or impure behaviors in components.
    - For example, ==if an impure component updates a variable during rendering, React will detect the issue due to the double render==.
  
3. **Example of Strict Mode Behavior**
    
   - In the case of an impure component, where a `count` variable is incremented during rendering, you may expect output like "Message 1", "Message 2", and "Message 3".
   - However, with Strict Mode enabled, React renders the component twice, resulting in output like "Message 2", "Message 4", and "Message 6".
   - The first render is used to detect potential issues, while the second render updates the UI.
  
4. **Console Logging in Strict Mode**
    
   - When logging in development mode with Strict Mode enabled, you’ll notice that some console logs appear twice. The logs from the second render are typically grayed out, indicating that they come from Strict Mode’s extra render pass.
    
        ![](assets/Pasted%20image%2020241003053924.png)
  
1. **Strict Mode in Development vs. Production**
    
    - **Strict Mode** is only active in **development mode**. When you build your application for production, these extra checks and double renders are not performed, and components render only once as expected.

- **Key Takeaways:**

  1. **Strict Mode** is a development tool in React that helps catch issues like side effects and impure components by rendering each component twice.
  2. It detects problems during the first render and updates the UI based on the second render.
  3. This behavior only affects development mode; in production, components will render only once.
  4. If your component behaves unexpectedly in development with Strict Mode, double-check for impure logic (like modifying variables during rendering).
---

# Updating Objects in React

1. **Grouping Related State Variables into Objects**
    
   - It’s a good practice to group related state variables into an object. For example, in the `App` component, you can create a `drink` object with properties like `title` and `price` using the state hook:
      ``` tsx 
      const [drink, setDrink] = useState({
        title: "Coke",
        price: 5 
      });
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/75b1e89c64a38d3ff4611fd85a10427f73685725/src/App.tsx)
        
2. **Immutability of State objects in React**
    
   - When updating an **State object** (or array) in React, you should **not directly modify** the original object. Instead, you must create a **new object** and update its properties.
   - **Example of an incorrect update**:
      ``` tsx 
      drink.price = 6; 
      setDrink(drink); // This won't work because React doesn’t detect the change.
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/a3815a322a15aa712d1d86fccf6ea9dd0eb4b9c3/src/App.tsx)
             
3. **Creating a New Object for Updates**
    
   - To inform React about state changes, you need to provide it with a **new object**. For example, instead of modifying the original `drink` object, you should create a new object:
      ``` tsx 
      const newDrink = { 
        title: drink.title,
        price: 6 };
      setDrink(newDrink);
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/b630242861b0b5ca1d24318774c41be21677c152/src/App.tsx)
   - Now, when the button is clicked, the `drink` object gets updated, and React re-renders the component with the new state.
  
4. **Using the Spread Operator for Efficiency**
    
   - Manually copying each property of an object can become tedious, especially if the object has many properties. Instead, you can use the **spread operator (`...`)** to copy the existing properties and update the necessary ones.
   - **Example**:
      ``` tsx 
      const newDrink = { ...drink, price: 6 };
      setDrink(newDrink);
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/9dcdfbc6f9f512e8b7034d5dc5e60e0e67a85ef7/src/App.tsx)
   - This spreads all the properties from the `drink` object into `newDrink` and updates the `price`.
  
5. **Inline Object Updates**
    
   - In simple cases, you can directly use the spread operator within the `setDrink` function without creating a separate object:
      ``` tsx 
      setDrink({ ...drink, price: 6 });
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/dd31dab0fbc7081389dfe20d46741fd1eab4d0f1/src/App.tsx)        
   - This is a more concise and clean way to update state in React.

- **Key Takeaways:**

  - **State in React is immutable**, meaning you should never directly modify the existing state objects.
  - ==Always create a **new object** when updating state object.==
  - Use the **spread operator (`...`)** to efficiently copy properties from the original object and update the necessary fields.
  - For simple updates, you can perform the update inline without creating a separate object.
---

