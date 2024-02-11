# Tuple

- Tuple is a fix size array which can contain multiple data types. (from `push` method we can change the length of the tuple also)

```js
//tuple is contain in this object
const person: {
  name: string,
  age: number,
  hobbies: string[],
  role: [number, string], //the way tuple define
} = {
  name: "Maximilian",
  age: 30,
  hobbies: ["Sports", "Cooking"],
  role: [2, "author"],
};
```

- If we try to assign number in the 2nd element of the tuple like this`person.role[1]=10` vs code show an error.
![](assets/Pasted%20image%2020240211101320.png)

- 