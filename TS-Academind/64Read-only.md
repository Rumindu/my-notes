# Read-only

- value can't be changed after initialization.
```js
class Department {
  constructor(public name: string, private readonly id: string) {}

  describe(this: Department) {
    console.log(`Department: ${this.name}: ${this.id}`);
  }
  addEmployee() {
     //this.id = "d2"; // Cannot assign to 'id' because it is a read-only property
  
  }
}
```