# React component exports / JS exports
- Mainly there is 2 types of export in js or React
  1. Default exports
  2. Name exports
## Default export
- don't need to put {}
- ex-
	```js
  // File: Parent.js
  const Parent = () => {
    return <div>Parent Component</div>
  };
  export default Parent;
	```

  ```js
  // File: App.js
  import AnyNameYouWant from './Parent';

  // You can now use AnyNameYouWant as a component
  ```
## Name export
- need to put {}
- ex-
```js
// File: child.js
// Named export
export const Child = () => {
  return <div>Child Component</div>
};
```

```js
// File: Parent.js
// Importing named export
import { Child } from './Child';
```
##
- read more from mdn reference JavaScript exports [export](https://developer.mozilla.org/en-US/docs/web/javascript/reference/statements/export) 
