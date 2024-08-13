# What is React

- React is a JavaScript library for building dynamic and interactive user interfaces.
- In React applications, we don’t query and update the DOM. Instead, we describe our application using small, reusable components. React will take care of efficiently creating and updating DOM elements
- React app is a tree of component, which `App` is root
    ![](assets/Pasted%20image%2020240724102251.jpg)
    ![](assets/Pasted%20image%2020240724101726.png)

# Create a react app
-  There is 2 ways to create react app
	1. Create React App
	2. Vite
- Here we are using ***Vite***. Because much faster and small bundle size
- create a react app using is Vite `npm create vite`.
- run Vite React project `npm run dev`
- [Github](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/29099e65f5d94de5da7ec8009703cfb16b29bc4d)

# Project structure
``` 
React-App
├───node_modules
├───public  //where public assets exsists(ex- images, video files) 
└───src //source code of application
│   │   App.css //styles for App component
│   │   App.tsx //App Component 
│   │   index.css //Global style for application
│   │   main.tsx
│   │   vite-env.d.ts
│   │
│   └───assets
│
│   index.html
│   package.json
│   package-lock.json
│   tsconfig.json
│   vite.config.ts
```

# Creating a react component
- React components can be created using a function or a class. Function-based components are the preferred approach as they’re more concise and easier to work with.
- ==JSX stands for JavaScript XML==. It is a syntax that allows us to write components that combine HTML and JavaScript in a readable and expressive way, making it easier to create complex user interfaces.
- This JSX code is compiled in to JS code. [babeljs.io/repl](https://babeljs.io/repl)
- Use **pascal casing** for naming components.
``` tsx 
//Message.tsx

//PascalCasing
function Message(){
  //JSX
  return <h1>Hello world</h1>
}

export default Message
```

``` tsx 
//App.tsx
import Messages from "./Message";

function App() {
  return <div> <Messages/> </div>;
}

export default App;
```
[Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/a8f9416457d0a434d18e30c45b5b4051e6fe41ee)

- Create dynamic content using JSX
  ``` tsx 
  //Message.tsx
  function Message(){
    const name ='Rumindu';
    if (name)
      return <h1>Hello {name}</h1>
    return <h1>Hello world</h1>
  }

  export default Message
  ```
[Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/5c3b77f3321d0406b75b00367e2a8388fad0a371)

# How React Works
- When our application starts, React takes a tree of components and builds a JavaScript data structure called the virtual DOM. This virtual DOM is different from the actual DOM in the browser. It’s a lightweight, in-memory representation of our component tree.
- When the state or the data of a component changes, React updates the corresponding node in the virtual DOM to reflect the new state. Then, it compares the current version of virtual DOM with the previous version to identify the nodes that should be updated. It’ll then update those nodes in the actual DOM.
- In browser-based apps, updating the DOM is done by a companion library called ==ReactDOM==. In mobile apps, React Native uses native components to render the user interface.
- Since React is just a library and not a framework like Angular or Vue, we often need other tools for concerns such as routing, state management, internationalization, form validation, etc.

| Library                                     | FrameWork                                       |
| ------------------------------------------- | ----------------------------------------------- |
| A tool that provides specific functionality | A set of tools and guidelines for building apps |
