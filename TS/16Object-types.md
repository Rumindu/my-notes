- By default we don't need to assign data type when we creating the objects.

```js
const person = {
  name: "Rumindu",
  age: 25,
};

console.log(person.name);
```

- But we can give the generic type `object` for the person object

```js
const person: object = {
  name: "Rumindu",
  age: 25,
};

console.log(person.name);
```

- but when we typed as object VS code can't get elements of the object
![](assets/Pasted%20image%2020240208074511.png)
- To prevent it we can define the type of object like below
```js
const person: {
  name: string,
  age: number,
} = {
  name: "Rumindu",
  age: 25,
};

console.log(person.name);
```
 - Therefore best Practice is doesn't specify type in the object. vs code automatically get type of object.
  ![](assets/Pasted%20image%2020240630222233.png)
  ![](assets/Pasted%20image%2020240208074848.png)
