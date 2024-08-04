# Inheritance

- No longer having dedicated constructor in sub class, base class's constructor will be inherit to the sub class.
1. Creating a subclass without having a dedicated constructor
```js
class Department {
  constructor(public name: string, private readonly id: string) {}

  describe(this: Department) {
    console.log(`Department: ${this.name}: ${this.id}`);
  }
}

class ITDepartment extends Department {
  admins: string[] = [];
  addAdmin(admin: string) {
    this.admins[0] = admin;
    console.log(this.admins);
  }
}

const Itdeparment = new ITDepartment("Accounting", "d1");
Itdeparment.addAdmin("Max");
```
- Here you can see even without having constructor, we need to pass parameters due to base class having a constructor

2. Creating a subclass with having a dedicated constructor
 ```js
 class Department {
  constructor(public name: string, private readonly id: string) {}
  describe(this: Department) {
    console.log(`Department: ${this.name}: ${this.id}`);
  }
}

class ITDepartment extends Department {
  admins: string[];
  constructor(id: string, admins: string[]) {
    super(id, "IT");
    this.admins = admins;
    console.log(this.admins);
  }
}

const Itdeparment = new ITDepartment("d1", ["Max"]);
Itdeparment.describe();

   
   ```
- ==super== - calling the constructor of the base class
- In the subclass constructor at very first line we must use super()(only base class has constructor)