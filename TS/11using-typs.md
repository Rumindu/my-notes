```js
function add(n1: number, n2: number) {//this is the how ts is used to define the type of the variable
  if (typeof n1 !== "number" || typeof n2 !== "number") {
    throw new Error("Incorrect input!");
  }
  return n1 + n2;
}

const number1 = 5;
const number2 = 2.8;

const result = add(number1, number2);
console.log(result);
```

- In TypeScript, you work with types like `string` or `number` all the times.

- **Important**: It is `string` and `number` (etc.), ==**NOT** `String`, `Number` etc.==. (not begin with Capital letter)

- The core primitive types in TypeScript are all **lowercase!**