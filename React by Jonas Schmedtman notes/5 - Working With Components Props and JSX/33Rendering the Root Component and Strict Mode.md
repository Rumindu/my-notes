**Starting React project from scratch**
* first delete those file created in React installing process
<img src="./Screenshot 2023-08-09 163831.png">
After we delete those files we get an error message
<img src="./Screenshot 2023-08-09 165618.png">
* we are going to create our first file inside `src` called `index.js`. we can't change this name because webpack of js looking index.js for start the project.
<img src='./Screenshot 2023-08-09 170001.png'>
<br>
* in  `index.js`
```js
import React from "react";
import ReactDOM from "react-dom/client";
```
* This `import` syntax directly come from java script under ES 6. In pure react lecture(in first section) we import those 2 files using `<script>` tag.

* Creating a first component
```js
import React from "react";
import ReactDOM from "react-dom/client";
//creating app component. It shouldn't want to be APP. 
//this is a convention. But component should start in upper case.
function App(){
  return <h1>Hello Reaact</h1>
}
```
* **Component name should start with upper case**
<br>
* Render the app component
```js
import React from "react";
import ReactDOM from "react-dom/client";
//creating app component. It shouldn't want to be APP. this is a convention. But component should start in upper case.
function App(){
  return <h1>Hello Reaact</h1>
}

//render the root React v18 (new version)
const root =ReactDOM.createRoot(document.getElementById("root"));//Here div id="root" is exsisting on ../public/index.html
root.render(<App/>);
```
<img src="./Screenshot 2023-08-09 174535.png">

<img src="./Screenshot 2023-08-09 174752.png">

<br>

**StrictMode** - render a component at twice
```js
const root =ReactDOM.createRoot(document.getElementById("root"));//Here div id="root" is exsisting on ../public/index.html
root.render(
<React.StrictMode> //adding strict mode for previous example
  <App/>
</React.StrictMode>

);
```
