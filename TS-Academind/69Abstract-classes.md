# Abstract classes

- In abstract methods Base class only has only name and return type of the method even it doesn't contain curly brackets. You have to implement the method in sub class.
```js
//To initiate abstract method we need abstract class
//Abstract classes can't be initiated directly. ex: const department = new Department("d1", "IT"); can't be done.
//only inherited class can be initiated. ex: const it = new ITDepartment("d1", ["Max"]);
abstract class Department {
  protected employees: string[] = [];

  constructor(protected readonly id: string, public name: string) {}

  //abstract method
  //abstract method can be created only in the abstract class
  abstract describe(): void;

  addEmployee(employee: string) {
    this.employees.push(employee);
  }

  printEmployeeInformation() {
    console.log(this.employees.length);
    console.log(this.employees);
  }
}

//inheriting class
//This class must implement the abstract method 'describe' from class 'Department
class ITDepartment extends Department {
  admins: string[];
  constructor(id: string, admins: string[]) {
    super(id, "IT");
    this.admins = admins;
  }

  describe() {
    console.log("IT Department - ID: " + this.id);
  }
}

const it = new ITDepartment("d1", ["Max"]);



```