# Add Bootstrap to project
- Install bootstrap `npm i bootstrap@5.2.3`
- Remove `index.css` from the `src` folder and import bootstrap by removing `import './index.css'` and add `import 'bootstrap/dist/css/bootstrap.css'` at `main.tsx`.
    ![](assets/Pasted%20image%2020240724125628.png)
    ![](assets/Pasted%20image%2020240724125607.png)
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
    // we should including markup within prentices
    //if there is multiple markup lines 
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
  // no need to put return markup within prentices
  //if only single line
  return <div><ListGroup /></div>
}

export default App;
```
- Get list group from [bootstrap documentation](https://getbootstrap.com/docs/5.3/components/list-group/). And replace `class` with `className`. Because `class` is reserved keyword in JS, therefore show a compile error.
- In React apps, a component can only return a single element. To return multiple elements, we wrap them in a fragment, which is represented by empty angle brackets(`<> </>`).
    ``` tsx 
    //ListGroup.tsx
    function ListGroup() {
    return (
        <>
        <h1>List</h1>
        <ul className="list-group">
            <li className="list-group-item">An item</li>
            <li className="list-group-item">A second item</li>
            <li className="list-group-item">A third item</li>
            <li className="list-group-item">A fourth item</li>
            <li className="list-group-item">And a fifth one</li>
        </ul>
        </>
    );
    }

    export default ListGroup;
    ```
---
# Rendering List using `map` function
- To render a list in JSX or TSX, we use the `array.map()` method. Because JSX/TSX doesn't have `for-loops`
- When mapping items to list, each item must have a unique key, which can be a string or a number. otherwise it will show an error on console.
    ``` tsx 
    //ListGroup.tsx
    function ListGroup() {
    const items = ["New York", "San Francisco", "Tokyo", "London", "Paris"];
    return (
        <>
        <h1>List</h1>
        <ul className="list-group">
            {/* must put map function within curly brackets */}
            {items.map((item) => (
            <li className="list-group-item">{item}</li>
            ))}
        </ul>
        </>
    );
    }

    export default ListGroup;
    ```
    ![](assets/Pasted%20image%2020240724150028.png)
- Mapping items to list with a unique key
``` tsx 
  //ListGroup.tsx
  function ListGroup() {
    ...
          {items.map((item) => (
            <li key={item} className="list-group-item">{item}</li>
          ))}
    ...
  }
  ```
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