# Private and Public Access modifiers

- When property or method became a **_private_** it can only access within in the **_class_**.
- follow the example will explain this

  1.  without having private

      ```js
      class Department {
        employees: string[] = [];

        addEmployee(employee: string) {
          this.employees.push(employee);
        }

        printEmployeeInformation() {
          console.log(this.employees.length);
          console.log(this.employees);
        }
      }

      const accounting = new Department();

      //adding employees in to the array using the method in class
      accounting.addEmployee("Max");
      accounting.addEmployee("Manu");

      //adding values the array using js inbuilt method
      accounting.employees[2] = "Anna";

      accounting.printEmployeeInformation();
      ```

      - Here we can enter value for the employees string array in 2 different ways. But we need form one specific way to do it. Then we convert employee array in to the **_private_** array.

  2.  Having a private array.

      ```js
      class Department {
      	//private array
      	private employees: string[] = [];

      	addEmployee(employee: string) {
      		this.employees.push(employee);
      	}

      	printEmployeeInformation() {
      		console.log(this.employees.length);
      		console.log(this.employees);
      	}
      }

      const accounting = new Department();

      accounting.addEmployee("Max");
      accounting.addEmployee("Manu");

      //now we can't access this array outside from the class.
      //accounting.employees[2] = "Anna";

      accounting.printEmployeeInformation();
      ```

- Here we can't access the employee array from the outside of the class. We need to use addEmployee() method to insert a value in to the array.