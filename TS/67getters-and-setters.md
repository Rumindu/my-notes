# Getters and setters
- getters==(get)== are using for get value from private properties and setters==(set)== are used for assign values for private properties
```js
class AccountingDepartment {
  private lastReport: string;
  //creating a getter
  //using for getting values of the private properties
  //getter methods has to return something
  //here we aren't passing any values as parameters
  get mostRecentReport() {
    if (this.lastReport) {
      return this.lastReport;
    }
    throw new Error("No report found.");
  }
  //setters
  //using for setting values to the private properties
  //getter and setter names can be equal or different. It isn't a matter
  set mostRecentReport(value: string) {
    if (!value) {
      throw new Error("Please pass in a valid value!");
    }
    this.addReport(value);
  }

  constructor(private reports: string[]) {
    this.lastReport = reports[0];
  }

  addReport(text: string) {
    this.reports.push(text);
    this.lastReport = text;
  }
}

const accounting = new AccountingDepartment([]);

accounting.addReport("Something went wrong...");

//accessing setter for assign a value for a private property.
accounting.mostRecentReport = "Year End Report";

//accessing data using getter
//even we calling for function we aren't using parenthesis. just like accessing property in a class
console.log(accounting.mostRecentReport);

```