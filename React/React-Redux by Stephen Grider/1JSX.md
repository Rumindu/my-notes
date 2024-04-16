# Learn about JSX & Component

- initiate project `npx create-react-app jsx`.
- Browser couldn't understand JSX.
- We transpile(convert code in to the another code formate) jsx in to the js.
  ![](assets/Pasted%20image%2020240405110338.png)

- Once we initiate a react project we can see so many files.
  ![](assets/Pasted%20image%2020240405110535.png)
  - Vast majority of those file don't run plain react project

- Out of those files we only need 5 main files to run our project
  ![](assets/Pasted%20image%2020240405112235.png)
  - Index.html file is contain on public folder

- This is the folder structure without unnecessary files.
  ![](assets/Pasted%20image%2020240405112820.png)

## Five Step process to create a component
 
- Those setup will be done on index.js
  ```js
  // 1) Import the React and ReactDOM libraries
  import React from 'react';
  import ReactDOM from 'react-dom';

  // 2) Create a react component
  const el = document.getElementById('root');

  // 3) Take the react component and show it on the screen
  const root = ReactDOM.createRoot(el); 

  // 4) Create a react component with JSX
  function App() {
      return (
          <h1> Hiiii</h1>
      );
  }

  // 5) Take the react component and show it on the screen
  root .render(<App />);
  ```
  
![](assets/Pasted%20image%2020240405114448.png)