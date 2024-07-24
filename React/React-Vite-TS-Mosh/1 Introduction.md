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
- Use **pascal casing** for naming components.
``` tsx 
//Message.tsx

//PascalCasing
function Message(){
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