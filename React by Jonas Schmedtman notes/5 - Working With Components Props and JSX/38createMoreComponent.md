* Create component with JSX
```js
function App(){
  return (
    <div>
    <h1>Hello Reaact</h1>
    <Header/>
    <Pizza/>
    <Pizza/>
    <Footer/>
    </div>
  );
  }

  function Header(){
    return <h1>First React company</h1>
  }
  function Footer(){
    return React.createElement('footer',null,"we are currently open") // without JSX only vanila JS
  }
```
* Create footer component with JSX
```js
function Footer(){
    return <footer>{new Date().toLocaleTimeString()}. We are currently open</footer>
    //footer is html element not Component name
    // {new Date().toLocaleTimeString()}- Entering js moode.
    // To do some js work. Get current time
  }
```
<img src="./Screenshot 2023-08-10 105051.png">

* nesting component further more
```js
function Menu(){
    //nesting Pizza component in menu component
    return <div>
              <h2>Our menu</h2>
                <Pizza/>
                <Pizza/>
                <Pizza/>
                </div>
}
```
Including `Menu` component in App component for preview it.
```js
function App(){
  return (
    <div>
    <h1>Hello Reaact</h1>
    <Header/>
    <Menu/>
    <Footer/>
    </div>
  );
  }
```
* Now we have same result but even more nested
<img src="./Screenshot 2023-08-10 110105.png">
