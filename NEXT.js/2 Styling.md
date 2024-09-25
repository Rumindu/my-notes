# Ways of styling Next.js application
- Global styles
- CSS modules
- Tailwind CSS
- Daisy UI
---
# CSS Modules
- **Definition**: CSS Modules are scoped CSS files that apply styles to a specific page or component, preventing styles from clashing or overriding each other across different parts of the application.
- **Problem Solved**: Traditional CSS can lead to class name collisions where classes defined in different places override each other. CSS Modules help solve this by making styles locally scoped.

- ## How CSS Modules Work:

- 1. **File Structure**:  
  - Create a `.module.css` file for each component.
  - Example: For a `ProductCard` component, name the CSS file `ProductCard.module.css`.

- 2. **Scoped Classes**:  
  - Define classes in the CSS module, which are scoped to that component only.
  - Example:
    ``` css 
    /* app/component/ProductCard.module.css */
    .card {
    padding: 1rem;
    border: 1px solid #ccc;
    }
    ```
  - The same class name can be defined elsewhere without conflicts.

- 3. **Importing CSS Modules**:
  - Import the CSS file in the component as a JavaScript object:
    ``` tsx 
    import styles from './ProductCard.module.css';
    ```
  - Access the class as a property of the `styles` object.
    ``` tsx 
    <div className={styles.card}></div>
    ```
    [Source code](https://github.com/Rumindu/next-app/blob/f9c59569ab94f0cba573874178b4d530d731644c/app/components/ProductCard.tsx)
                
- ## **Important Notes**:

- **Naming Conventions**:  
  - CSS module **class names** must follow **camelCase** because hyphens (`-`) are not valid JavaScript property names.
  - For example, use `cardContainer` instead of `card-container`.
- **Unique Class Names**:  
  - When rendered in the browser, class names are auto-generated using **PostCSS** to avoid collisions.
  - PostCSS transforms class names into unique identifiers (e.g., `card_x7ks23`).
    ![](assets/Pasted%20image%2020240925041642.png)
  - The project typically uses `postcss.config.js` to manage these transformations with plugins like **Tailwind** and **Autoprefixer**.

- ## **Folder Structure**:

  - You can group your component and its CSS in the same folder for better organization.
  - Example:
    ``` 
        ProductCard/   
          ProductCard.tsx 
          ProductCard.module.css
    ```

- **CSS Modules can also be applied to pages, creating styles specific to individual pages, just like components.**.
---

# Tailwind
- Example : styling a `dev`
  ``` tsx 
  <div className="p-5 my-5 bg-sky-400 text-white text-xl hover:bg-sky-500">
  ```
  [Source code](https://github.com/Rumindu/next-app/blob/8e5e82562de70ca0dc0abd55e716ecaabca63da4/app/components/ProductCard.tsx)

---

# Daisy UI
- **Daisy UI** is most popular **component library for tailwind.** like bootstrap for tailwind
- ## [Configure Daisy UI](https://daisyui.com/docs/install/)
1. Install daisyUI as dev dependencies `npm i -D daisyui@latest`.
2. Add daisyUI to tailwind.config.js:
   ``` json
    //...
    plugins: [
      require('daisyui'),
    ],
   ```
   [source code](https://github.com/Rumindu/next-app/blob/bef76127bf13fe61956c7ef6a3b583ca0d9fd2c8/tailwind.config.ts)
- example: [button component](https://daisyui.com/components/button/)
  ``` tsx 
  //app/components/AddToCart.tsx
  <button className="btn btn-primary" onClick={() => console.log("Click")}>
  ```
  [source code](https://github.com/Rumindu/next-app/blob/bef76127bf13fe61956c7ef6a3b583ca0d9fd2c8/app/components/AddToCart.tsx)
  ![](assets/Pasted%20image%2020240925060622.png)
- ## [daisyUI themes](https://daisyui.com/docs/themes/)
1. adding theme in tailwind config file
   ``` json
   // ...
   daisyui: {
    themes: ["winter"],
   ```  
2. apply theme for html element. here we apply html element in layout file.
   ``` tsx 
   <html lang="en" data-theme="winter">
   ```
   [source code](https://github.com/Rumindu/next-app/blob/bef76127bf13fe61956c7ef6a3b583ca0d9fd2c8/app/layout.tsx)
- ## Implement [table](https://daisyui.com/components/table/) using daisyUI
- shortcut to when creating table
  
  ![](assets/Pasted%20image%2020240925062409.png)
  
  ![](assets/Pasted%20image%2020240925062432.png)
  [source code](https://github.com/Rumindu/next-app/blob/bef76127bf13fe61956c7ef6a3b583ca0d9fd2c8/app/users/page.tsx)
  