- File path of all code snippets `src/components/ListGroup/Form.tsx`
# Building a Form in React

1. **Setting up the form:**
    
   - Create a new component for the form using a function component.
   - Use **Bootstrap classes** for styling:
     - Example: `mb-3` for margin-bottom and `form-control` for input fields.
   - **Shortcut to generate div with Bootstrap properties**:
     - In VS Code, type the **class** and press **Tab** to generate the HTML. Example:
       - `div.mb-3>label.form-label+input.form-control`
          ![](assets/Pasted%20image%2020241008210626.png)
       - This will auto-generate the div, label, and input with the proper Bootstrap classes.
          ![](assets/Pasted%20image%2020241008210713.png) 
2. **Form structure:**
    
   - Inside the div, add:
     - A **label** with the class `form-label`.
     - An **input** with the class `form-control`.
   - For accessibility:
     - ==Use the **`htmlFor`** attribute on the label and match it to the **id** of the input.==
     - Then the user clicked on the label, input will automatically focused 
     - Example: `<label htmlFor="name">Name</label>` and `<input id="name" />`.
  
3. **Testing the form:**
    
   - Import the form into the **App** component and render it.
   - Add **padding** to the body to prevent the form from being too close to the screen edges:
     - Inside `src` folder add a new file `index.css` for global styles of React project.
     - Example:
        ``` css
        body { 
		      padding: 20px; 
        }
        ```
     - Import `index.css` in `main.tsx`.

4. **Adding input fields:**
    
      - Repeat the structure to add more fields.
      - **Use shortcuts** to generate Bootstrap-marked divs quickly. Example:
        - `div.mb-3>label.form-label+input.form-control[type=number]`
      - Set the input type where needed (e.g., `type="number"` for numeric inputs).
      - Example: `<input type="number" id="age" className="form-control" />` and corresponding label `<label htmlFor="age">Age</label>`.

5. **Form validation:**
    
   - Numeric input fields accept only numbers (letters are not allowed).

6. **Adding a submit button:**
    
   - After the input fields, add a **submit button** using Bootstrap button classes:
    
    ![](assets/Pasted%20image%2020241008213048.png)
    
    ![](assets/Pasted%20image%2020241008213107.png)
    
     - Example:
        ``` tsx 
        <button type="submit" className="btn btn-primary">Submit</button>
        ```
        [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/011b3117dcef3906c3a2685a816c4460001edd0d/src/components/ListGroup/Form.tsx)
---

# Handling Form Submission 

1. **Handling form submission:**
    
   - To handle form submission in React, use the `onSubmit` event on the form element, similar to handling button clicks.
      ``` tsx 
      <form onSubmit={()=>console.log("submitted")}>
      ```
        
   - Initially, logging messages to the ==console might disappear== because the form performs a full-page reload upon submission. This is the default behavior in HTML.
  
2. **Prevent default behavior:**
    
   - To stop the form from refreshing the page, call `event.preventDefault()`.
      ``` tsx 
      <form
        onSubmit={(event) => {
          event.preventDefault();
          console.log("submitted");
        }}
      >
      ```      
   - This ensures that the form won't be posted to the server, and the log message will persist in the console.

3. **Refactoring into a separate function:**
    
   - If the logic within the `onSubmit` event handler becomes complex, move it to a separate function for better code organization.
     - Define a separate function called `handleSubmit`:
      
      ![](assets/Pasted%20image%2020241009050700.png)
      - Here we need to define type of event. TS compiler couldn't assign a type like when this implement as the `onSubmit`'s prop
         
         ![](assets/Pasted%20image%2020241009051111.png)
   
   - Define the type of the `event` parameter as `FormEvent`from the React module 
      ``` tsx
      //Import `FormEvent` from the React module
      import React, { FormEvent } from "react";
      //... 

      //annotate the `event` parameter.
      const handleSubmit = (event: FormEvent) => {
         event.preventDefault();
         console.log("submitted");
      };
      ```
    - **Reference** `handleSubmit` function in the `onSubmit` event. **not calling just a referencing**. It means don't type braces`()` after the function name
      ``` tsx 
      <form onSubmit={handleSubmit}>
      ```
---

# Accessing Input Fields using the `useRef` hook:

1. **The `useRef` hook:**
    
   - React provides the `useRef` hook to reference DOM elements directly.
   - To reference an input field, import `useRef` and call it with an initial value of `null`. Reason for initial value being null is explain in point 7
      ``` tsx 
      import { useRef } from 'react';
      // ...
      //useRef returns the reference object
      const nameRef = useRef<HTMLInputElement>(null);
      ```
        
2. **Associating the ref with an input field:**
    
   - Use the `ref` attribute to link the `useRef` object with the input field.
      ``` tsx 
      <input ref={nameRef} id="name" ... />
      ```

        
3. **Accessing the input value:**
    
   - Upon form submission, access the input value using the `current` property of the ref object.
   - The input field's value can be retrieved through `nameRef.current.value`.
  
      ![](assets/Pasted%20image%2020241009070512.png)
   
   - To prevent getting this error Handle null-checks to ensure `nameRef.current` is not `null`.
      ``` tsx
      if (nameRef.current !== null) {
         console.log(nameRef.current.value); 
      }
      ```
        
4. **Dealing with TypeScript:**
    
   - TypeScript requires specifying the type of the element being referenced. In this case, use `HTMLInputElement`.
   - Without specifying, TypeScript will throw an error (e.g., `Property 'value' does not exist on type 'never'`).
      
      ![](assets/Pasted%20image%2020241009070830.png)
   
   - To prevent getting this error
      ``` tsx 
      const nameRef = useRef<HTMLInputElement>(null);
      ```
        
5. **Repeating for multiple input fields:**
    
   - Repeat the process for additional inputs, such as for age:
      ``` tsx 
      const ageRef = useRef<HTMLInputElement>(null);
      // ....
      <input ref={ageRef} />
      ```
   - Access the value the same way and convert to the necessary type if needed (e.g., `parseInt` for numbers).
  
6. **Creating an object to send:**
    
   - Typically when submitting the form, we need to send and object to the server to be save. Therefore instead of logging values individually, create an object to store the input values.
      ``` tsx 
      const person = { name: "", age: "" };
      const handleSubmit = (event: FormEvent) => {
         event.preventDefault();
         if (nameRef.current !== null) {
         person.name = nameRef.current.value;
         }
         if (ageRef.current !== null) {
         person.age = parseInt(ageRef.current.value);
         }
         console.log(person)
      };
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/c8c835d434e4f0fd8aa0b472e5262b8ff2d2cec4)
        
7. **Why initialize with `null`:**
    
   - React's DOM is created after the component renders, so there’s no DOM node to reference at the time of initialization.
   - Always initialize ref objects with `null` to avoid issues, as the `current` property will later be updated by React when the DOM node is rendered.
   - This avoids unexpected behavior when referencing DOM nodes.

8. **Personal opinion (Mosh):**
    
   - Mosh mentions that initializing the ref object with `null` is cumbersome and could have been handled better by React itself, as it feels like a design flaw. However, it’s necessary to follow this approach due to how React handles DOM nodes.
--- 

# Accessing Input Fields using the `useState`:
- Video name "5- Controlled Components"
1. **Using the `useState` hook:**
    
   - Instead of using the `useRef` hook to get input values, you can use the `useState` hook to control the form’s state. 
   - Initialize a state object (e.g., `person`) with properties like `name` and `age`.
      ``` tsx 
      const [person, setPerson] = useState({ name: '', age: '' });
      ``` 
        
2. **Handling the `onChange` event:**
    
   - Each input field has an `onChange` event that fires every time the user types.
   - Use this event to update the corresponding state property when a user types in the input field. [update state object](./4%20Managing%20component%20state#Updating%20State%20Objects%20in%20React)
   - For example, to update the `name` field:
      ``` tsx 
      <input
         type="text"
         value={person.name}
         onChange={(event) => setPerson({ ...person, name: event.target.value })}
      />
      ```
   - Similarly, for `age`. But here we need to `parseInt()` target's value:
  
      ![](assets/Pasted%20image%2020241017051043.png)

      ``` tsx 
      <input
         type="number"
         value={person.age}
         onChange={(event) => setPerson({ ...person, age: parseInt(event.target.value) || '' })}
      />
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/d9050cf460d06677b59929e12ef53a8506c9202d/src/components/ListGroup/Form.tsx)
        
3. **Controlling the component state:**
    
    - React maintains the state, and each keystroke updates the corresponding state variable.
    - The component is re-rendered whenever the state is updated. While some argue this could impact performance, it usually isn’t a significant issue for most forms.

4. **Single source of truth:**
    
   - To avoid input fields and state becoming out of sync, set the `value` attribute of the input fields to the state variables (`person.name` and `person.age`).
   - This ensures React controls the state of the input fields, making them "controlled components":
      ``` tsx 
      <input type="text" value={person.name} onChange={...} />
      <input type="number" value={person.age} onChange={...} />
      ```
        
5. **Handling initial state issues:**
    
   - By default, setting the `age` field to `0` displays the number `0` in the input box, which can be undesirable.
  
      ![](assets/Pasted%20image%2020241017051459.png)

	- To solve this, initialize `age` as an empty string instead of `0` and remove `parseInt` form age's input field:
      ``` tsx 
      const [person, setPerson] = useState({ name: '', age: '' });
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/653ce1f3f003009d16334acab6cb344949e97875/src/components/ListGroup/Form.tsx)
      
      ![](assets/Pasted%20image%2020241017060635.png)
      
6. **Submitting the form:**
    
   - On form submission, log or us  e the `person` object:
      ``` tsx 
      const handleSubmit = (event: FormEvent) => {
         event.preventDefault();
         console.log(person);
      };
      ```
        
7. **Controlled vs uncontrolled components:**
    
   - A controlled component is one where React manages the input state through state variables.
   - This approach ensures that the form's data is always consistent and easier to manage.

8. **Performance considerations:**
    
   - While some advocate for using `useRef` in performance-critical situations, Mosh advises against premature optimization unless the form becomes complex and performance issues arise.
---

# Forms with React Hook Form

1. **Introduction to React Hook Form:**
    
   - Managing form state with `useState` can become tedious as forms grow complex. Every input field requires both `onChange` and `value` attributes.
   - `React Hook Form` simplifies form handling by reducing the amount of code.
   - Install the library: `npm install react-hook-form@7.43`
        
2. **Using `useForm` Hook:**
    
   - Start by importing and using the `useForm` hook from React Hook Form.
      ``` tsx 
      import { useForm } from "react-hook-form";
      const { register, handleSubmit } = useForm();//handleSubmit explain on point 6
      ```     
   - The `useForm` hook returns an object containing various properties and methods to handle form functionality, such as `register`, `reset`, `setError`, and more.

3. **Registering Input Fields:**
    
   - To register an input field, use the `register` function provided by `useForm`.
   - This function attaches necessary event handlers like `onBlur`, `onChange`, and a `ref`, without needing to explicitly set `value` or `onChange` attributes:
      ``` tsx 
      console.log(register("name"));
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/2d9a5d9ac55f809e7c93f5940a9724007f8ddb47/src/components/ListGroup/Form.tsx)

      ![](assets/Pasted%20image%2020241017120054.png)
      
   - We pass input field's id as an argument to the `register` function and it will return the object which contain `onBlur`, `onChange`, and a `ref` properties. To get those properties as props of `<input>` we spread the object using spread operator(.`...register("id_of_input_fileld")`).   
      ``` tsx 
      <input {...register("name")} />
      <input {...register("age")} />
      ```

4. **Avoiding Re-renders:**
    
   - React Hook Form uses `ref` objects to manage form values, meaning it avoids re-rendering the component every time a user types, which makes it more efficient compared to the traditional `useState` approach.

5. **Removing Unnecessary Code:**
    
   - Since React Hook Form handles state internally, you no longer need to use `useState` to manage the form state.
   - You also don't need to write `onChange` handlers or use the `value` attribute for each field.
      ``` tsx 
      const { register } = useForm(); // No need for useState to store person object
      ```
        
6. **Handling Form Submission:**
    
   - React Hook Form provides a `handleSubmit` function, which you can use to manage form submission.
   - You pass it a callback function that receives the form data as its argument:
      ``` tsx
      // ... 
      const { register, handleSubmit } = useForm();;
      // ...
      <form onSubmit={handleSubmit(data=>console.log(data))}>
         <input {...register("name")} />
         <input {...register("age")} />
         <button type="submit">Submit</button>
      </form>
      ```
      [source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/2d9a5d9ac55f809e7c93f5940a9724007f8ddb47/src/components/ListGroup/Form.tsx)
        
7. **Real world application and TypeScript Considerations:**
   
    - In real world application there is more than console log. Therefore we implement this logic in separate function like `onSubmit`.
    - In TypeScript, when defining the `onSubmit` function, you might encounter a type error. The form data is typed as `FieldValues` by default, which you can use to annotate the data parameter:
      
      ![](assets/Pasted%20image%2020241017115437.png)
      
      ``` tsx 
      import { FieldValues } from "react-hook-form";
      //....
      const onSubmit = (data: FieldValues) => {
         console.log(data);
      };
      //....
      <form onSubmit={handleSubmit(onSubmit)}>

      ```
      [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/8b6ee528e5d3cde5968b3acfc9ed82d90fa3a0b7/src/components/ListGroup/Form.tsx)
    
        
8. **Advantages:**
    
    - **Less code:** React Hook Form significantly reduces the amount of boilerplate code needed for managing forms.
    - **Performance:** By using `refs`, it avoids unnecessary re-renders, making it more efficient, especially for large forms.