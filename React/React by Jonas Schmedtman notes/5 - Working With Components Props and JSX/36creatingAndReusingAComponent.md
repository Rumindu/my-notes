# Creating and reusing a component

* In react we are creating *Components* using *functions*.
* In React there is 2 important 2 rules, when we create Components as Function.
  1. First function name start with **Uppercase**.
  2. Function needs to **return** some **markup**. usually in the form of JSX. But we can return `null` also. Here just return `<h2>`
```js
function Pizza(){
  return <h2>Pizza</h2>
}
```
but nothing will appear in UI. Because we aren't including this component any where. Even `ESLint` Vs code extension also warn us by yellow line.

![](assets/Screenshot%202023-08-09%20222440.png)

* So we should include `Pizza` component in `App` component. Because `App component` is currently rendering on screen. (If u can't remember this fact refer 33Rendering the Root Component and Strict Mode.)

```js
//This Including is wrong. error is occuring
function App(){
  return <h1>Hello Reaact</h1><Pizza/>//using component Pizza
  
}
```
<h2>wrong</h2>

* But here occurring an error. **Because Component can only return one element**.

* so we wrap those `element`s using `<div>`
  
  
```js
import React from "react";
import ReactDOM from "react-dom/client";

  function App(){
  //wrapping <h1> and <pizza/> using <div>
  return (
    <div>
    <h1> Hello Reaact </h1> 
    <Pizza/>
    </div>
  );
  }

function Pizza(){
  return <h2>Pizza</h2>
}

const root =ReactDOM.createRoot(document.getElementById("root"));
root.render(
<React.StrictMode>
  <App/>
</React.StrictMode>
);
```
![](assets/Screenshot%202023-08-09%20231134.png)
* Here we are **nested** `Pizza` component in the `App` component. 
* we should **never write a function inside another function** as nesting.

## Adding a image and paragraph to Pizza component 
* All the assets of the app *like images* will go into the **public folder**. Because webpack/module bundler will automatically get them from there.

```js
function Pizza(){
  return( 
  <div>  
    <h2>Pizza spinaci</h2>
    <img src="pizzas/spinaci.jpg" alt="pizza"></img> //adding an image
    <p>Tomato, mozarella, spinach, and ricotta cheese</p>
  </div>
  );
}
```
![](assets/Screenshot%202023-08-09%20234210.png)
## Reusing Components

```js
//3 times adding above component
function App(){
  return (
    <div>
    <h1>Hello Reaact</h1>
    <Pizza/>
    <Pizza/>
    <Pizza/>
    </div>
  );
  }

```

![](assets/Screenshot%202023-08-09%20234548.png)
