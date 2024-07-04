# Singleton private constructor

- Singleton pattern - there is only one instance of a class
```js
class AccountingDepartment {
  private employees: string[] = [];
  //declare a variable to assign the intense of the class
  private static instance: AccountingDepartment;
  //here constructor is private
  private constructor(public id: string) {}
  //here method
  static getInstance() {
    if (AccountingDepartment.instance) {
      return this.instance;
    }
    //Because constructor is private we can access it only inside the class
    this.instance = new AccountingDepartment("d2");
    return this.instance;
  }

  describe() {
    console.log("Accounting Department - ID: " + this.id);
  }

  addEmployee(name: string) {
    if (name === "Max") {
      return;
    }
    this.employees.push(name);
  }
  printEmployeeInformation() {
    console.log(this.employees.length);
    console.log(this.employees);
  }
}

//Due to the constructor is private in AccountingDepartment we can't use new key word for instantiate the class. class is only accessible from inside the class
//const accounting = new AccountingDepartment('d2', []);
const accounting = AccountingDepartment.getInstance();
const accounting2 = AccountingDepartment.getInstance();
accounting.addEmployee("Rumindu");
accounting2.addEmployee("Kavindu");
accounting2.printEmployeeInformation();
accounting.printEmployeeInformation();

```
those are the console logs
![](assets/Pasted%20image%2020240304220045.png)
Here we can clearly see only one instance is created even two time initiate the class.