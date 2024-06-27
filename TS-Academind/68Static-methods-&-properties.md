# Static methods and properties

- To access static properties and methods in a class we don't need to instantiate a class using new key word. We can access those static methods and properties directly on the class.
- ex-
```js
math.pow() 
//here we arn't initiate instence of a math class. just class_name.method_name
```

```ts
class Department {
  //static property
  static fiscalYear = 2020;

  constructor(protected readonly id: string, public name: string) {}
  //static method
  static createEmployee(name: string) {
    return { name: name };
  }
}
//accessing static method
const employee1 = Department.createEmployee("Max");
console.log(employee1)

//accessing static property
console.log(Department.fiscalYear);
```

- Inside the class  also we can't access static properties using this keyword. we can access using class_name.property_name.
```ts
class Department {
  static fiscalYear = 2020;

  constructor(protected readonly id: string, public name: string) {
    //console.log(this.fiscalYear) //error
    console.log(Department.fiscalYear);
  }

  static createEmployee(name: string) {
    console.log(Department.fiscalYear);
    //or can access using this keyword inside static method only
    console.log("this keyword",this.fiscalYear);
    return { name: name };
  }
}
```