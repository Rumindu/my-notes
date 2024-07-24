# Add Bootstrap to project
- Install bootstrap `npm i bootstrap@5.2.3`
- Remove `index.css` from the `src` folder and import bootstrap by removing `import './index.css'` and add `import 'bootstrap/dist/css/bootstrap.css'` at `main.tsx`.
    ![](assets/Pasted%20image%2020240724125628.png)
    ![](assets/Pasted%20image%2020240724125607.png)

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