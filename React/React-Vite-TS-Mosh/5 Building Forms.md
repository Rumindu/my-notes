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

# Note on Handling Form Submission 

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
    - **Reference** `handleSubmit` function in the `onSubmit` event. **not calling just a referencing**. It means not put `()` after the function name
      ``` tsx 
      <form onSubmit={handleSubmit}>
      ```
---