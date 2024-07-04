- Union datatype is a type formed from two or more other types,
- Simple example

```js
let value: number | string;

value = 123; // OK
value = "123"; // OK
value = true; // Error: Type 'boolean' is not assignable to type 'number | string'
```

- In below example we again checked type of input variables Otherwise TS compiler show error.
```js
//Here input1 and input2 has union data type
function combine(input1: number | string, input2: number | string) {
  let result;
  if (typeof input1 === "number" && typeof input2 === "number") {
    result = input1 + input2;
  } else {
    result = input1.toString() + input2.toString();
  }
  return result;
}

const combinedAges = combine(30, 26);
console.log(combinedAges);

const combinedNames = combine("Max", "Anna");
console.log(combinedNames);
```
