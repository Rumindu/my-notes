# Class
- to run ts compiler in watching mode `tsc -w`
- convention to the naming class is
	1. Use a noun for naming it
	2. Begin from a capital letter

- Sample class
```js
class Department {

  //this is how you declare a property or field in a class
  name: string;

  //constructor of the class
  constructor(n: string) {
    //this is how you access the property of the class and initialising it
    this.name = n;
  }
}

//Instantiating the class "Department"
const accounting = new Department("Accounting");
console.log(accounting);
```
- console log
![](assets/Pasted%20image%2020240223120606.png)

## Accessing method in a class

```js
class Department {
  division: string;
  constructor(n: string) {
    this.division = n;
  }
  describe() {
    console.log("Department: " + this.division);
    //Here "this" key word is compulsory
  }
}

const accounting = new Department("Accounting");

//accessing the public method
accounting.describe();
```

- *** To access the properties of the class we need to use ***"this"*** keyword