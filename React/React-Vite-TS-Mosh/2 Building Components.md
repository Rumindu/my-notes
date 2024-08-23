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
- To conditionally render content, we can use an `if statement` or a `ternary` operator or `&&` operator.
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
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/dd5da8fff9e6f77fe8a215ea78b76283acacf379)
  
#### 2. Ternary operation ( `? :`)
- Inside JSX we can't use `if statements`. 
- Using `ternary` operations we can do conditional rendering inside JSX.
- Inside the JSX we can only use html element or other react component. Only exception is `{ }` curly braces. Here we can render anything dynamically. 
	``` tsx 
  //ListGroup.tsx
  function ListGroup() {
    ...
    return (
      <>
        <h1>List</h1>
        {/* if this condition is true return <p>No item found</p> */}
        {/* else return null, null means nothing would be render. */}
        {items.length === 0 ? <p>No item found</p> : null}
        <ul className="list-group">
          ...
        </ul>
      </>
    );
  }
    ...

  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/fb3fc7951f8a2312701935d3bd5072cefd3b141d)

- Sometimes this logic be more complicated and unreadable JSX . For those cases we extract this logic and store in a variable or constant. And include variable/constant name within `{ }` in JSX.
  ``` tsx 
  //ListGroup.tsx
  function ListGroup() {
    ...
    //store condition in variable
    const message = items.length === 0 ? <p>No item found</p> : null

    return (
      <>
        <h1>List</h1>
        {/*render the constant*/}
        {message}
        ...
      </>
    );
  }

  export default ListGroup;

  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/570ef703f3f501373e1bc238157d5434b9ce2e7b)

- we can move above logic inside the function. And calling the function within `{}` in JSX. Benefit of using function is we can get different parameters depending on condition and rendering items according to those.
  ``` tsx 
  //ListGroup.tsx
  function ListGroup() {
    ...
    //declare function which returns logic
    const getMessage = ()=>{
      return items.length === 0 ? <p>No item found</p> : null
    }

    return (
      <>
        <h1>List</h1>
        {/* calling the functon */}
        {getMessage()}
        ...
      </>
    );
  }
  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/feafb844cdda27d85c2fcd7b858211f36eb3945e)

#### 3. &&
- Mostly common use way for Conditional rendering
- If our condition is true result will be paragraph element. But if the condition is false, result of entire expression is false and nothing would be render on the screen. 
  ``` tsx 
  {/* "logic" && "value that return when condition is true" */}
  {items.length ===0 && <p>No item found</p>}
  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/0ca0d089ab62658500e545582bba65b35996f1c3)
- explain how it works using console on chrome development tools.
  ![](assets/Pasted%20image%2020240725135650.png)
---
# Handle events
- Here we see handle **Click event** on the component.
- Clicked on each item of the list and get a out put in the console. In React each html has property called `onClick`.
  ``` jsx 
  //ListGroup.tsx
  <li
      key={item}
      className="list-group-item"
      onClick={() => console.log("Clicked")}
    >
  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/61a60a1370acec961ccca8030626e0bdfab30ae4/src/components/ListGroup.tsx)
  ![](assets/Pasted%20image%2020240820192554.png)
- Need to get clicked item name on console
  ``` tsx 
  {items.map((item) => (
    <li
      key={item}
      className="list-group-item"
      onClick={() => console.log(item)}
    >
      {item}
    </li>
  ))}

  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/b2ae1716503502003b4db5865c24985fbd4af783/src/components/ListGroup.tsx)
  ![](assets/Pasted%20image%2020240820195805.png)
- When we mapping an items we can optionally add second parameter as `index`. From this we can see index of item we clicked.
  ``` tsx 
  {items.map((item,index) => (
    <li
      key={item}
      className="list-group-item"
      onClick={() => console.log(item,index)}
    >
      {item}
    </li>
  ))}
  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/f5f0ed2b769672c5b096d318907e324fad102521/src/components/ListGroup.tsx)
  ![](assets/Pasted%20image%2020240820205704.png)
- Arrow function, which is calling on `onClick` can optionally has parameter that represent browser event. We can called it `e` or `event`. let's log it on console and see what we can see.
  ``` tsx 
  onClick={(e) => console.log(e)}
  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/26791b6d6b24f8f46652d0efc7446f9e0994d107/src/components/ListGroup.tsx)
  ![](assets/Pasted%20image%2020240820212659.png)
- Type of this object is `SyntheticBaseEvent` which wrapped around around browser event object. This is built in class in React. Reason for having this is cross browser compatibility.
  ![400](assets/SmartSelect_20240820_213351_Samsung%20Notes.jpg)
- Here event handling logic is very simple. If the logic is more complex we don't write the logic middle of the JSX markup. We move the logic in to separate function.
  ![](assets/SmartSelect_20240820_220352_Samsung%20Notes.jpg)
- We need to specify the type of the parameter `event`. If we hover the mouse over the `event` parameter in JSX we can see the type. 
  ![](assets/Pasted%20image%2020240820221311.png)
- When we pass `event` in inline JSX function TS compiler knows type of the parameter. That's why we don't get any warning earlier
- But when we declare separate function TS compiler doesn't know type of parameter.
- Once we put the type annotation we will get properties of event object from IntelliSense.
  ![](assets/Pasted%20image%2020240820224121.png)
  ``` tsx 
  //must be import
  import { MouseEvent } from "react";

  function ListGroup() {
    //Event handler
    //the job is handling the event in this case click events
    const handleClick=(event:MouseEvent)=>console.log(event)

    return (
      <>
        ...
          <li
            key={item}
            className="list-group-item"
            // don't put () when calling event handler
            onClick={handleClick}
          >
            {item}
          </li>
        ...
      </>
    );
  }
  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/67d074c7df6c9a336f091b4d38f4c90735f33a87/src/components/ListGroup.tsx)
---

# Managing State
- We want to highlight item when it's clicked. To achieve that we add `active` class from bootstrap to the list item with a conditional rendering. Next we need a variable to track  on index of clicked list item. And need a function to set value of declared variable to the index of clicked item
  ``` tsx 
  function ListGroup() {
    //clicked item tracking variable
    // let selectedIndex = -1 means no item is clicked
    let selectedIndex = 0;// by default 1st item is clicked

    return (
      ...
        <li
          key={item}
          className={
            // apply active class with conditional rendering
            index === selectedIndex
              ? "list-group-item active"
              : "list-group-item"
          }
          onClick={() => {
            // updating value of tracking variable
            selectedIndex = index;
          }}
        >
          {item}
      </li>
    ...
    );
  }
  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/7aaefc728037c3343393ad9ef8d00d67fc918b2c/src/components/ListGroup.tsx)
- But clicked item isn't highlighting as we expected.
- The Reason is `selectedItem` variable is local to `ListGroup` component. This is like little secret inside component. So React isn't aware of when it's value change. 
- To solve this issue we should tell react that this component  is going to have data/state that might change over time.
- To do that we have to use one of in built function in React called `useState`. Prior to use it we must import.
  ``` tsx 
  import { useState } from "react";
  ```
- `useState` is a example for a Hook in React.
- Hook is a function that allows us to tap into built in features in React.
- Using the `useState`hook we can tell react that this component has data/state that will change overtime.
- So instead of declaring a variable, we are going to call `useState` function with passing the initial value of variable want to be and the `useState` returns an array.
  ``` tsx 
  const arr = useState(-1)
  ```
- In this `arr` we are going to have 2 elements. 1st element is going to be a value which passed in to `useState`. And 2nd element is going to be updater function.
  ``` tsx 
  const arr = useState(-1);
  arr[0] //variable like SelectedIndex value with -1
  arr[1] //updater function
  ```
- Using updater function we can update `arr[0]` variable. At that point React will be notified. So React knows that the state/data of our component is changed. And then React will re render our component which cause the DOM to update under the hood.
  ``` tsx 
  import { useState } from "react";

  function ListGroup() {
    const arr = useState(-1);
    console.log(arr[0]); //-1 at initial rendering
    return (
      <>
        ...
          <li
            key={item}
            className={
              // apply active class with conditional rendering
              index === arr[0] ? "list-group-item active" : "list-group-item"
            }
            onClick={() => {
              // updating value of arr[0] using updater function
              arr[1](index);
            }}
          >
            {item}
          </li>
        ...
    );
  }
  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/070cf37bd8a66a24b7864fbba26be32ba7637369/src/components/ListGroup.tsx)
- Instead of working 2 individual elements easier to destructor the array into elements.
  ``` tsx 
  const [selectedIndex, setSelectedIndex] = useState(-1);
  ```
- The convention of naming elements is `const[state_variable,setState_variable]`.
  ``` tsx 
  import { useState } from "react";

  function ListGroup() {

    //Here we can use let instead of const. 
    //But using const helps prevent accidental reassignments
    //and makes the code easier to understand.
    const [selectedIndex, setSelectedIndex] = useState(-1);
    return (
      <>
        ...
          <li
            key={item}
            className={
              // apply active class with conditional rendering
              index === selectedIndex
                ? "list-group-item active"
                : "list-group-item"
            }
            onClick={() => {
              // updating state variable.
              setSelectedIndex(index);
            }}
          >
            {item}
          </li>
        ...
    );
  }
  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/700bb24e43ad30b80911d23f84d50e67cac67f29/src/components/ListGroup.tsx)
- Each component has its own state.
- To explain that add another `ListGroup` component in the `App` component.
  ``` tsx
  function App() {
    return <div> <ListGroup/><ListGroup/></div>;
  }
  ```
  [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/adbd8fd033f9081c83f8b181a067f893132c2991/src/App.tsx)
  ![](assets/Pasted%20image%2020240823124209.png)
- Here we can see each `<ListGroup>` has its own state. First `<ListGroup>`'s selected item isn't selected on 2nd `<ListGroup>`. There will be independent on each other.