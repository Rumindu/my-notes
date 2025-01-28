# Spread operator vs Rest operator
- Spread and rest both use the same `...` syntax, but they do opposite things depending on where they appear: [freecodecamp-javascript-rest-vs-spread-operators](https://www.freecodecamp.org/news/javascript-rest-vs-spread-operators/).
# Object de structuring with providing new variable names.
``` js 
const o = { p: 42, q: true };
const { p: foo, q: bar } = o;

console.log(foo); // 42
console.log(bar); // true

```
[MDN Object destructuring assigning to new variable names](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#assigning_to_new_variable_names)
[TS object destructuring](https://www.typescriptlang.org/docs/handbook/variable-declarations.html#object-destructuring)