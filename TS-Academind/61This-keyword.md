# "this"

1. To refer a class property or method inside the class, we need to use 'this' keyword.
  ```js
  class Department {
    name: string;

    constructor(n: string) {
      this.name = n;
    }

    describe() {
      //to refer a class property or method inside the class, we need to use 'this' keyword
      console.log("Department: " + this.name);
    }
  }

  const accounting = new Department("Accounting");
  accounting.describe();
  ```

  ![](assets/Pasted%20image%2020240303111725.png)

2. "this" key word can be tricky
	ex-

  ```js
  class Department {
    name: string;

    constructor(n: string) {
      this.name = n;
    }

    describe() {
      console.log("Department: " + this.name);
    }
  }

  const accounting = new Department("Accounting");
  accounting.describe();

  // creating an object (not an instance of the class)
  const accountingCopy = { describe: accounting.describe };

  accountingCopy.describe(); // this will print "Department: undefined"
  //reason for being undefined is that the describe method is called on the accountingCopy object, but the method is not bound to the accountingCopy object, but to the accounting object. So the this keyword will refer to the accountingCopy object, which does not have a name property.
  //"this" typically refers to the thing which is responsible for calling the method. Here responsible for calling the method is accountingCopy object, Because "accountingCopy.describe" is called. So "this" refers to accountingCopy object. But accountingCopy object does not have name property. So it is undefined.
  ```
![](assets/Pasted%20image%2020240303132854.png)

  - To prevent above ambiguity

  ```js
  class Department {
    name: string;

    constructor(n: string) {
      this.name = n;
    }
    //here this: Department is used to tell that this method is called on an object/instance of Department class. It is a dummy parameter but it behave for extra type safety.
    describe(this: Department) {
      console.log("Department: " + this.name);
    }
  }

  const accounting = new Department("Accounting");
  accounting.describe();
  //Property 'name' is missing in type '{ describe: (this: Department) => void; }' but required in type 'Department'.ts(2684)
  //const accountingCopy = { describe: accounting.describe };

	//there for here we passing value for name propert
  const accountingCopy = { name: "sample_department", describe: accounting.describe };
  accountingCopy.describe();

  ``` 
  ![](assets/Pasted%20image%2020240303134825.png)