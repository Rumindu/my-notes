# Simple shopping cart
## Dependencies
1. react-router-dom
 2. bootstrap 
 3. react-bootstrap

## Developing

- Add bootstrap to the index.tsx `import "bootstrap/dist/css/bootstrap.min.css";`

- Folder structure in the `src` folder
  ```
  ├── App.css
  ├── App.tsx
  ├── components
  ├── context    // for react and redux
  ├── data        // storing json data
  ├── hooks     //custom local hooks
  ├── index.css
  ├── index.tsx
  ├── pages     // (high-level route)
  └── utilities   //use functions like formatting currency...
  ```

- Routing part using `import { BrowserRouter } from 'react-router-dom';` in the `index.tsx`
  ```js
  const root = ReactDOM.createRoot(
    document.getElementById('root') as HTMLElement
  );
  root.render(
    <React.StrictMode>
      <BrowserRouter> 
      <App />
      </BrowserRouter> 
    </React.StrictMode>
  );
  ```

- All of the routes are including in the `app.tsx`
  ```js
  import { Route, Routes } from "react-router-dom";
  import {Container} from "react-bootstrap";

  function App() {
    return (
      <Container> {/*Component from the react bootstrap for styling*/}
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/store" element={<Store />} />
          <Route path="/about" element={<About />} />
        </Routes>
      </Container>
    );
  }

  export default App;
  ```
  
- When we add styles for the container it will applied for the all the pages in the routes component
  ```js
  <Container className="mt-4"> {/*adding some margin from the top*/}
  ```

- Navbar component is common to the all page therefore we are placing it at the `App.ts`.
  ```js
  import {Navbar} from "./components/Navbar";

  function App() {
    return (
      <>  
      <Navbar />{/*Navbar component is added here*/}
      <Container className="mb-4">
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/store" element={<Store />} />
          <Route path="/about" element={<About />} />
        </Routes>
      </Container>
      </>
    );
  }
  ```
- Creating component Navbar in the Component folder
  ```js
  import {Container, Navbar as NavbarBs} from "react-bootstrap";
  //Because function name is also Navbar, we need to rename the import component
  export function Navbar(){
    return <NavbarBs className="big-white shadow-sm mb-3"> 
      <Container>Nav
      {/*"Nav" will be replace by original code*/}
      </Container>
    </NavbarBs>
  }
  ```
- After inserting links in to the `Navbar` component
  ```js
  import {Container, Nav, Navbar as NavbarBs} from "react-bootstrap";
  import { NavLink } from "react-router-dom";

  export function Navbar(){
    return <NavbarBs className="big-white shadow-sm mb-3"> 
      <Container>
        <Nav>
          <Nav.Link to={"/"} as={NavLink}>Home</Nav.Link>
          {/* When you use as={NavLink} with Nav.Link, you're telling Nav.Link to render as a NavLink. This means it will have the styles of Nav.Link and the routing and active styling capabilities of NavLink. */}
          <Nav.Link to={"/store"} as={NavLink}>Store</Nav.Link>
          <Nav.Link to={"/about"} as={NavLink}>About</Nav.Link>
        </Nav>
      </Container>
    </NavbarBs>
  }
  ```

- Store page mobile responsiveness from bootstrap classes