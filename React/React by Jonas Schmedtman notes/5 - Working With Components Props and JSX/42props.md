# Props
* How we pass data between components. Specially **Parent** component to **Child** component. 

 ```js
 //parent component
function Menu() {
  return (
    <div>
      <h2>Our menu</h2>
      <Pizza
        //passing value in to prop.
        name='Pizza Spinachi'
        ingredient='Tomato, mozarella, spinach, and ricotta cheese'
        photoName='pizzas/spinaci.jpg'
        price='10'
      />
    </div>
  );
}

//child component
function Pizza(po) {
  console.log(po);
  .
  .
  .
 ```
 * console output
 ![](assets/Screenshot%202023-08-10%20134446.png)
 
 * simply says parent component is calling `piza` function with passing object. Here console contain this object.
 <br>
 * **getting value from object using js** 
 ```js
 //parent component
function Menu() {
  return (
    <div>
      <h2>Our menu</h2>
      <Pizza
        //passing value in to prop.
        name='Pizza Spinachi'
        ingredient='Tomato, mozarella, spinach, and ricotta cheese'
        photoName='pizzas/spinaci.jpg'
        price='10'
      />
    </div>
  );
}

//child component
function Pizza(po) {
  return (
    <div>
      {/* getting value from object using js this is the way to put comment in return */}
      <h2>{po.name}</h2>
      <img src={po.photoName} alt={po.name}></img>
      <p>{po.ingredient}</p>
    </div>
  );
}
 ```
 * Creating another pizza item in menu reuing `pizza` component just passing values.
 ```js
 function Menu() {
  return (
    <div>
      <h2>Our menu</h2>
      <Pizza
        //passing value in to prop.
        name='Pizza Spinachi'
        ingredient='Tomato, mozarella, spinach, and ricotta cheese'
        photoName='pizzas/spinaci.jpg'
        price='10' 
        {/* if we assign a number {1} use curly bracket and enter number inside */}
      />
      {/* Creating another pizza reusing same component */}
      <Pizza
        //passing value in to prop.
        name='Pizza Funghi'
        ingredient='Tomato, mozarella, spinach, and ricotta cheese'
        photoName='pizzas/funghi.jpg'
        price='12'
      />
    </div>
  );
}


function Pizza(po) {
  return (
    <div>
      <h2>{po.name}</h2>
      <img src={po.photoName} alt={po.name}></img>
      <p>{po.ingredient}</p>
    </div>
  );
}
 ```
 * methanadi pizza 2k output karnawa
