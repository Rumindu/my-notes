```js
const person = {
  name: "Rumindu",
  age: 25,
  hobbies: ["Sports", "Cooking"],
};

//Declare a array and after assigning values to it
let favoriteActivities: string[];
favoriteActivities = ["Sports"];

//applying for loop to the array
for (const hobby of person.hobbies) {
  console.log(hobby.toUpperCase());
  // console.log(hobby.map()); // !!! ERROR !!! because map is not a method of string.("hobby" is a atring)
}
```
