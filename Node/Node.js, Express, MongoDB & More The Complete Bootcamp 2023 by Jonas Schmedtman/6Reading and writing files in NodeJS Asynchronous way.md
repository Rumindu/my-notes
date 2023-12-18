# Asynchronously read and write a file

## Read a file
* To read a file asynchronously we need `readFile()` function in **fs** module.
* we need to pass
	1.  file path which is need to read
	2. file encoding type
	3. **call back function** - we call this 'call back' function with 2 arguments.
		1. err
		2. data
		```js
				(err, data1) => {console.log(data1);} // here always error should be in the first
		```

```js
const fs = require('fs');

fs.readFile('./txt/start.txt', 'utf-8', (err, data1) => {
console.log(data1);

});
```
****Output***
![](./assets/Pasted%20image%2020231218164723.png)

* Here at first 'start.txt' is reading in the background. While this process is running background rest of the code executing procedurally. Once it completes node will call to the **call back** function mentioning in here. (*We should pass those arguments according to the above order*). below code phrase will further more explain this process

```js
const fs = require('fs');
fs.readFile('./txt/start.txt', 'utf-8', (err, data1) => {
	console.log(data1);
});
console.log('Will read file!');
```
***
****Output***
	![asynchronous console output](./assets/Pasted%20image%2020231218155921.png)
\* Here we can see, after the 'will read file!' console logging the content of the text file.
## Asynchronous function within an Asynchronous function
```js
fs.readFile('./txt/start.txt', 'utf-8', (err, data1) => {
  fs.readFile(`./txt/${data1}.txt`, 'utf-8', (err, data2) => {
    console.log(data2);
  });
});
console.log('Will read file!');
```
****Output***
![](./assets/Pasted%20image%2020231218170416.png)

## Read and Write files asynchronously

```js
const fs = require('fs');

fs.readFile('./txt/start.txt', 'utf-8', (err, data1) => {
  fs.readFile(`./txt/${data1}.txt`, 'utf-8', (err, data2) => {
    console.log(data2);

    fs.readFile('./txt/append.txt', 'utf-8', (err, data3) => {
      console.log(data3);
		//writing file asynchronusly.
      fs.writeFile('./txt/final.txt', `${data2}\n${data3}hiiiii`, 'utf-8', err => {
        console.log('Your file has been written!');
      });
    });
  });
});
console.log('Will read file!');
```
* **node.js built around call backs**

## what happen the reading file doesn't exist

```js
	fs.readFile('./txt/startsad.txt', 'utf-8', (err, data1) => {
  	if (err) return console.log('ERROR! 💥');
	});
	console.log('Will read file!');
```
****Output***
![](./assets/Pasted%20image%2020231218174503.png)

