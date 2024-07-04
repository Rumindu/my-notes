# Shorthand-form to specify private or public access modifier.

- Conventional way
```js
class Department {
  name: string;
  private id: string;

  constructor(name: string, id: string) {
    this.name = name;
    this.id = id;
  }

  describe(this: Department) {
    console.log(`Department: ${this.name}: ${this.id}`);
  }
}

const accounting = new Department("Accounting", "d1");

accounting.describe();
```

- Shorthand way
```js
class Department {
  constructor(public name: string, private id: string) {}

  describe(this: Department) {
    console.log(`Department: ${this.name}: ${this.id}`);
  }
}

const accounting = new Department("Accounting", "d1");

accounting.describe();
```

- *** Here we also should mention "public" keyword prior to the public properties.
- 