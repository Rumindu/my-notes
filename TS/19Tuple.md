# Tuple

- Tuple is a fix size array which can contain multiple data types. (from `push` method we can change the length of the tuple also)

```js
//this object contain a tupple
const person: {
  name: string,
  age: number,
  hobbies: string[],
  //****the way tuple define**
  role: [number, string],
} = {
  name: "Maximilian",
  age: 30,
  hobbies: ["Sports", "Cooking"],
  role: [2, "author"],
};
```

- If we try to assign number in the 2nd element of the tuple like this
	```js
	 person.role[1]=10
	 ```
 - vs code show an error.
	  ![](assets/Pasted%20image%2020240211101320.png)

- But when we try to add an element to the tuple using ***push method*** it will work.
	```js
	person.role.push("admin");
	```