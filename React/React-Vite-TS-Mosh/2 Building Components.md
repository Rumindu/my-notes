# Add Bootstrap to project
- Install bootstrap `npm i bootstrap@5.2.3`
- Remove `index.css` from the `src` folder and import bootstrap by removing `import './index.css'` and add `import 'bootstrap/dist/css/bootstrap.css'` at `main.tsx`.
    ![](assets/Pasted%20image%2020240724125628.png)
    ![](assets/Pasted%20image%2020240724125607.png)
[Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/7168d758bbc0e6be736df2cd511ab175ad04101d)
---
# Create List group component
- By convention all the component will store on `components` folder in  the `src`.
- Here create `ListGroup.tsx` file.
``` 
    src
    │   App.css
    │   App.tsx
    │   main.tsx
    │   vite-env.d.ts
    │
    ├───assets
    │       react.svg
    │
    └───components
            ListGroup.tsx
```

``` tsx 
//ListGroup.tsx
function ListGroup() {
  return (
    //if there is multiple markup lines  we should including markup within prentices
    <ul className="list-group">
      <li className="list-group-item">An item</li>
      <li className="list-group-item">A second item</li>
      <li className="list-group-item">A third item</li>
      <li className="list-group-item">A fourth item</li>
      <li className="list-group-item">And a fifth one</li>
    </ul>
  );
}

export default ListGroup;
```

``` tsx 
//App.tsx
import ListGroup from "./components/ListGroup";

function App() {
  //if there is only single line no need to put return markup within prentices
  return <div><ListGroup /></div>
}

export default App;
```
[Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/6d6653990d7aa0048ffd0b26658f16d1c23b270d)
- Get list group from [bootstrap documentation](https://getbootstrap.com/docs/5.3/components/list-group/). And replace `class` with `className`. Because `class` is reserved keyword in JS, therefore show a compile error.

---
# Fragment
- In React apps, a component can only return a single element. To return multiple elements, we have 3 solutions
- ### Solution 1 - Wrap both `<h1>` and `<ul>` inside `<div>`
- VS code shortcut for doing this wrapping
  ![](assets/SmartSelect_20240814_100710_Samsung%20Notes.jpg)
  ![](assets/Pasted%20image%2020240814100824.png)
  ![](assets/SmartSelect_20240814_101050_Samsung%20Notes.jpg)
  ``` tsx 
  //ListGroup.tsx
  ...
  return (
    <div>
      <h1>List</h1>
      <ul className="list-group">
        <li className="list-group-item">An item</li>
        <li className="list-group-item">A second item</li>
        <li className="list-group-item">A third item</li>
        <li className="list-group-item">A fourth item</li>
        <li className="list-group-item">And a fifth one</li>
      </ul>
    </div> 
  );
  ...
  ```

  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/fd2b2f3cdd8ff981d0e4f141c1a8eb95cff0bf63)
  - Here we added an extra one element for DOM only for the happiness of React. This is unnecessary. Better way is use fragment.

- ### 2) Solution 2 - `<Fragment>`
  ``` tsx 
  //ListGroup.tsx
  //importing Fragment component
  import { Fragment } from "react";

  function ListGroup() {
    return (
      <Fragment>
        <h1>List</h1>
        <ul className="list-group">
          <li className="list-group-item">An item</li>
          ...
        </ul>
      </Fragment> 
    );
  }
  ...
  ```

  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/1a354cda4ac27aa52f726c78dad45e0e4f106b3f)

- ### 3) Solution 3 - <> </>
  - Don't need to import `Fragment` from React and just replace `<Fragment>` by `<>`. Here `Fragment` is represented by angle brackets(`<> </>`).

  ``` tsx 
  //ListGroup.tsx
  function ListGroup() {
  return (
      <>
      <h1>List</h1>
      <ul className="list-group">
          <li className="list-group-item">An item</li>
          ...
      </ul>
      </>
  );
  }

  export default ListGroup;
  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/919a67fe9b6cb10e1511509d25fdf7b483cb4f35)
  
---

# Rendering List using `map` function
- To render a list in JSX, we use the `array.map()` method. Because JSX doesn't have `for-loops`
  ``` tsx 
  function ListGroup() {
    //declare const and store String array
    const items = ["New York", "San Francisco", "Tokyo", "London", "Paris"];
    return (
        <>
        <h1>List</h1>
        <ul className="list-group">
            {/* must put map() function within curly brackets */}
            {items.map((item) => (
            // {item} should be within {} to render data dynamically 
            <li className="list-group-item">{item}</li>
            ))}
        </ul>
        </>
    );
  }
  export default ListGroup;
  ```
- In above implementation we get an warning message on console.
	![](assets/Pasted%20image%2020240724150028.png)
- When mapping items to list, React needs unique key for each item, which can be a string or a number. otherwise it will show an error on console.
- Mapping items to list with a unique key
  ``` tsx 
  //ListGroup.tsx
  function ListGroup() {
  ...
    {items.map((item) => (
    // Here we can use item as unique key,
    //Because each item is unique String
    <li key={item} className="list-group-item">
      {item}
    </li>
    ))}
  ...
  }
  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/8c1218381fe948a32fca11c492639d198db4c9bc)

---
# Conditional Rendering
- To conditionally render content, we can use an ‘if’ statement or a ternary operator or && operator.
#### 1. If statement
- Not much use because due to code duplication.
  ``` tsx 
  //ListGroup.tsx
  function ListGroup() {
    let items = ["New York", "San Francisco", "Tokyo", "London", "Paris"];
    items = [];
    if (items.length === 0)
      return (
        <>
          <h1>List</h1>
          <p>No item found</p>
        </>
      );
    return (
      <>
        <h1>List</h1>
        <ul className="list-group">
          {items.map((item) => (
            <li key={item} className="list-group-item">
              {item}
            </li>
          ))}
        </ul>
      </>
    );
  }

  export default ListGroup;
  ```
#### 2. Ternary operation
- Inside JSX we can't use `if statements`. 
  ``` tsx 
  //ListGroup.tsx
  function ListGroup() {
    let items = ["New York", "San Francisco", "Tokyo", "London", "Paris"];
    items= [];
    return (
      <>
        <h1>List</h1>
        {/* if this condition is true return <p>No item found</p> */}
        {/* else return nothing. */}
        {items.length === 0 ? <p>No item found</p> : null}
        <ul className="list-group">
          {items.map((item) => (
            <li key={item} className="list-group-item">
              {item}
            </li>
          ))}
        </ul>
      </>
    );
  }

  export default ListGroup;
  ```

-  Sometimes this logic be more complicated and unreadable JSX . For those cases we extract this logic and store in a variable.
  ``` tsx 
  //ListGroup.tsx
  function ListGroup() {
    let items = ["New York", "San Francisco", "Tokyo", "London", "Paris"];
    items = [];
    
    //store condition in variable
    const message = items.length === 0 ? <p>No item found</p> : null

    return (
      <>
        <h1>List</h1>
        {/*render the constent*/}
        {message}
        <ul className="list-group">
          {items.map((item) => (
            <li key={item} className="list-group-item">
              {item}
            </li>
          ))}
        </ul>
      </>
    );
  }

  export default ListGroup;
  ```
- we can move above logic into function also
  ``` tsx 
  //ListGroup.tsx
  function ListGroup() {
    let items = ["New York", "San Francisco", "Tokyo", "London", "Paris"];
    items= [];

    //store condition in variable
    const getMessage = ()=>{
      return items.length === 0 ? <p>No item found</p> : null
    }

    return (
      <>
        <h1>List</h1>
        {/* calling the functon */}
        {getMessage()}
        <ul className="list-group">
          {items.map((item) => (
            <li key={item} className="list-group-item">
              {item}
            </li>
          ))}
        </ul>
      </>
    );
  }

  export default ListGroup;
  ```

#### 3. &&
- Mostly common use way for Conditional rendering
  ``` tsx 
  {/* "logic" && "value that return when condition is true" */}
  {items.length ===0 && <p>No item found</p>}
  ```
- explain how it works using console on chrome development tools
  ![](assets/Pasted%20image%2020240725135650.png)
---