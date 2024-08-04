# Overriding and protected attributes

- We can override base class properties and methods in sub classes.
- If the access modifier is ***private*** we can't access those properties in the base class. But if the access specifier is ***protected*** sub classes can access those properties. 
```js
class Department {
  //protected attributes
  protected employees: string[] = [];
  constructor(private readonly id: string, public name: string) {}

  describe(this: Department) {
    console.log(`Department (${this.id}): ${this.name}`);
  }

  addEmployee(employee: string) {
    this.employees.push(employee);
  }

  printEmployeeInformation() {
    console.log(this.employees.length);
    console.log(this.employees);
  }
}

class AccountingDepartment extends Department {
  constructor(id: string, private reports: string[]) {
    super(id, "Accounting");
  }
  // overriding the addEmployee method in the base class
  addEmployee(name: string) {
    if (name === "Max") {
      return;
    }
    //accessing protected attributes in the sub class 
    this.employees.push(name);
  }

  addReport(text: string) {
    this.reports.push(text);
  }

  printReports() {
    console.log(this.reports);
  }
}


const accounting = new AccountingDepartment("d2", []);

accounting.addReport("Something went wrong...");

accounting.addEmployee("Max");
accounting.addEmployee("Manu");

accounting.printReports();
accounting.printEmployeeInformation();



```