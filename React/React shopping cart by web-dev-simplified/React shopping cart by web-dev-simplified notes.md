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
  ```js
  import { Col, Row } from "react-bootstrap";
  import storeItem from "../data/items.json"
  export function Store() {
    return (
      <>
        <h1>Store</h1>
        <Row md={2} xs={1} lg={3} className="g-3">{storeItem.map(item=>(<Col>{JSON.stringify(item)}</Col>))}
        {/*"md={2} xs={1} lg={3}" for at the medium screen size 2 columns, extra small size 1 column and large size 3 columns */}</Row>
      </>
    );
  }
  ```
- For formatting currency we use  `formatCurrency,ts` file on `utilities` folder
  ```js
  const CURRENCY_FORMATTER = new Intl.NumberFormat(undefined, {
    currency: "USD",
    style: "currency",
  })

  export function formatCurrency(number: number) {
    return CURRENCY_FORMATTER.format(number)
  }
  ```
- Basic structure of `StoreItem` component
  ```js
  import { Button, Card } from "react-bootstrap";
  import { formatCurrency } from "../utilities/formatCurrency";
  import { useState } from "react";

  type StoreItemProps = {
    id: number;
    name: string;
    price: number;
    imgUrl: string;
  };

  export function StoreItem({ id, name, price, imgUrl }: StoreItemProps) {
    const [quantity, setQuantity] = useState(1);
    return (
      <Card className="h-100">
        <Card.Img
          variant="top"
          src={imgUrl}
          height="200px"
          //for doesn't stretching the image and being center od the container
          style={{ objectFit: "cover" }}
        />
        <Card.Body className="d-flex flex-column">
          <Card.Title className="d-flex justify-content-between align-items-baseline mb-4">
            <span className="fs-2">{name}</span>
            <span className="fs-2">{formatCurrency(price)}</span>
          </Card.Title>
          <div className="mt-auto">
            {quantity === 0 ? (
              <Button className="w-100">+ Add to Cart</Button>
            ) :
            (
              <div className="d-flex align-items-center flex-column" style={{ gap: ".5rem" }}>
                <div className="d-flex align-items-center justify-content-center" style={{ gap: ".5rem" }}>
                <Button>-</Button>
                <div>
                  <span className="fs-3">{quantity}</span>
                  in cart
                </div>
                <Button>+</Button>
                </div>
                <Button variant="danger"> Remove </Button>
              </div>
            )}
          </div>
        </Card.Body>
      </Card>
    );
  }
  ```
  - React Context - feature in React that allows you to share values between components without having to pass props.
- Local Storage using custom hook called `useLocalStorage` 