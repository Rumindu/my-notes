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

# Updating State Objects in React

- When updating objects or arrays, we should treat them as immutable objects. Instead of mutating them, we should create new objects or arrays to update the state

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
   - ==**Example of an incorrect update**:==
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
  
5. ==**Inline Object Updates**==
    
   - In simple cases, you can directly use the spread operator within the `setDrink` function without creating a separate object:
      ``` tsx 
      setDrink({ ...drink, price: 6 });
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/dd31dab0fbc7081389dfe20d46741fd1eab4d0f1/src/App.tsx)        
   - This is a more concise and clean way to update state in React.

-  **Key Takeaways:**

  1. **State in React is immutable**, meaning you should never directly modify the existing state objects.
  2. ==Always create a **new object** when updating state object.==
  3. Use the **spread operator (`...`)** to efficiently copy properties from the original object and update the necessary fields.
  4. For simple updates, you can perform the update inline without creating a separate object.
---

# Updating Nested Objects in React

1. **Creating a Nested Object in State**
    
   - In this example, the state is a `customer` object that has nested properties, like `name` and `address`. The `address` itself is another object with properties like `city` and `zipCode`.
      ``` tsx 
      const App = () => {
      const [customer, setCustomer] = useState({
				name: "John Doe",
				address: { city: "New York", zipCode: "10001" },
      });
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/dd8cd284d2e19112ec81b2870d77070a811cade4/src/App.tsx)

2. **The Spread Operator and Shallow Copy**
    
   - When updating a nested object, we use the **spread operator** to copy properties from the existing object. However, the spread operator performs a **shallow copy**, meaning it only copies references to nested objects, not the objects themselves.
   - If you use the spread operator like this:
      ``` tsx 
      const newCustomer = { ...customer };
      ```    
   - Both the original and new `customer` objects will still reference the **same `address` object in memory**, which is unsuitable when updating state.
  
3. **Ensuring State Independence**
    
   - To ensure that the **new state object is independent** from the original state object (i.e., they don't share references to nested objects), we need to create a new object for the nested structure as well.
   - When updating the `zipCode`, we should:
     1. Spread the properties of the original `customer` object.
     2. Create a **new `address` object** and spread the existing properties from the original `address`.
     3. Update the specific field (`zipCode`) in the new `address` object.
   
4. **Example of Correctly Updating Nested State**
    
   - Here’s how to properly update the `zipCode`:
      ``` tsx 
      setCustomer({
      ...customer, // Spread the existing customer object
      address: {   // Create a new address object
         ...customer.address, // Spread the existing address object
         zipCode: "94112"     // Update the zipCode
      }
      });
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/185df2ed79c5e90c6edac8ce38b1d06e5700feef/src/App.tsx)
   - This ensures that the new `customer` object has a new `address` object and doesn't reference the old one, making the state update **fully independent**.
  
5. **Avoiding Deeply Nested Structures**
    
    - Mosh emphasizes that when working with state in React, **deeply nested structures** should be avoided. The more nested the object, the more complex the update logic becomes.
    - **Flattening the state** or keeping a simpler structure makes it easier to manage and update.

- **Key Takeaways:**

  1. The **spread operator** in JavaScript performs a **shallow copy**, meaning nested objects are still shared between copies.
  2. When updating nested state, ensure **independence** by creating new objects for any nested structures.
  3. Avoid deeply nested state structures to reduce complexity and simplify update logic in React.
---

# Updating State Arrays in React

1. **Creating an Array in State**
    
   - The `useState` hook can be used to store an array in a React component.
      ``` tsx 
      const [tags, setTags] = useState(["happy", "sad", "excited"]);
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/5d2d6dc78ee3efae0b3e753a36194a27aa9ee42b/src/App.tsx)
             
2. **Adding Items to an Array**

   - We don't modify the original array using methods like `.push()`.    
   - To **add** a new item to the array, we create a new array by **spreading** the existing array and appending the new item:
      ``` tsx 
      setTags([...tags, "cheerful"]);
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/1766db7552ed317f318f67faeba2eb453416ddcd/src/App.tsx)
        
3. **Removing Items from an Array**
    
   - To **remove** an item from an array, use the `.filter()` method, which returns a new array with only the items that meet the condition:
      ``` tsx 
      setTags(tags.filter((tag) => tag !== "sad"));
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/1766db7552ed317f318f67faeba2eb453416ddcd/src/App.tsx)
   - This ensures that the original array is not mutated and React gets a new array object to track.
  
4. **Updating Items in an Array**
    
   - If you need to **update** a specific item in the array, the `.map()` method is useful. This method creates a new array by iterating over each item, allowing you to modify the item that matches your condition:
      ``` tsx 
      setTags(tags.map((tag) => (tag === "excited" ? "thrilled" : tag)));
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/1766db7552ed317f318f67faeba2eb453416ddcd/src/App.tsx)
   - In this example, it changes `"happy"` to `"happiness"` while leaving other items unchanged.

- **Key Takeaways**

  1. When working with arrays in React state, **never mutate the original array**. Always create a new array using methods like **spread**, **filter**, or **map**.
  2. Use the **spread operator** to copy existing items when adding or modifying arrays.
  3. Use `.filter()` to **remove** items from an array.
  4. Use `.map()` to **update** specific items in the array.
---

# Updating a State Array of Objects in React

1. **Array of Objects in State**
    
   - You can use the `useState` hook to store an array of objects in a React component. For example:
		``` tsx 
		const [bugs, setBugs] = useState([
			{ id: 1, title: "Bug 1", fixed: false },
			{ id: 2, title: "Bug 2", fixed: false },
		]);
		```
            
2. **Updating an Object in an Array**
    
   - To update a specific object in the array (like marking a bug as fixed), we need to follow these steps:
     - Use the `.map()` method to **create a new array**.
     - Inside `.map()`, check the condition to identify the object you want to update (e.g., using `id`).
     - For the object that needs to be updated, create a **new object** using the **spread operator** to copy existing properties and override the specific property (e.g., `fixed`).
     - For other objects, return them as they are.
     - Example of marking the first bug as fixed:
		``` tsx 
		setBugs(bugs.map((bug) => (bug.id === 1 ? { ...bug, fixed: true } : bug)));
		```
		[source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/9948636d02e8058a16e94a24e44ff9914cad70de/src/App.tsx)
        
3. **Visualizing the Update**
    
   - Initially, we have two bug objects: `B1` and `B2`. After the click event, a **new array** is created where:
     - `B1` is replaced with `B1*` (a new object with `fixed: true`).
     - `B2` remains unchanged. This process ensures that React detects changes to the array and only re-renders the part of the DOM corresponding to the updated object.
			
		![](assets/Pasted%20image%2020241007194118.png)
  
4. **Key Point**
    
    - You don't need to create a brand new copy of every object in the array. Only the object that needs modification (in this case, `B1`) is replaced with a new one. The rest of the objects remain the same.

- **Key Takeaways:**

  - Use `.map()` to iterate over the array and identify the object to update.
  - Create a **new object** for the one that needs changes, using the **spread operator** to copy existing properties and override specific fields.
  - React only re-renders the part of the DOM that corresponds to the updated object, optimizing performance.
---

# Simplifying Update Logic with Immer

1. **Why Use Immer?**
    
   - Updating arrays and objects immutably in React can be complex and repetitive. Immer simplifies this process by allowing mutations on a **draft** version of the state, while keeping the actual state immutable behind the scenes.

2. **Installation**
    
   - First, install Immer using:
		``` bash 
		npm install immer
		```
    
3. **Example: Updating an Array of Bugs**
    
    - The task is to mark the first bug in an array of bugs as "fixed" when a button is clicked.

4. **Using Immer in React**
    
   - Import the `produce` function from Immer:
		``` tsx 
		import produce from "immer";
		```
        
   - Instead of mapping through the bugs array and creating new objects, Immer allows you to directly modify a **draft** of the state:
		``` tsx 
		setBugs(
			produce((draft) => {
				const bug = draft.find((bug) => bug.id === 1);
				if (bug) {
					bug.fixed = true;
				}
			})
		)
		```
		[source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/7a8956444f5d1752af506990aecda16c989f1184/src/App.tsx)
         
5. **How It Works**
    
    - The `produce` function takes a function that receives **draft**, a **proxy object** representing a mutable version of the state.
    - You can directly mutate this **draft** as if it were a regular JavaScript object. Behind the scenes, Immer keeps track of the changes and applies them immutably, creating a new state object.
  
6. **Rendering the State**
    
   - To visualize the changes, iterate through the `bugs` array and conditionally render "fixed" or "new" based on the bug’s state:
		``` tsx 
		{bugs.map((bug) => {
			return (
				<p key={bug.id}>
					{bug.title} {bug.fixed ? "Fixed" : "New"}
				</p>
			);
		})}
		```
		[source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/7a8956444f5d1752af506990aecda16c989f1184/src/App.tsx)