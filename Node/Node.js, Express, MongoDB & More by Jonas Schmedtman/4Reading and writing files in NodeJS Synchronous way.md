* to proceed this we need **node module**. (All kind of additional functionalities are stored in modules )
* To use those modules we need to require those relevant modules and store in variables.
```js
const fs = require('fs'); //here 'fs' stand for file system
 ```
 * `fs` module give access for **reading and writing data in to file system**
 * `require('fs')` return an object it contain so many functions and it store in `fs` variable. 
 * [more details about file system](https://nodejs.org/dist/latest-v20.x/docs/api/fs.html)
# Reading text from a text file (Synchronous way )

```js
const fs =require ('fs');

//readFileSync() used for read entier file Synchronously 
//need to pass 'file path' and 'character encoding' type as parameters
const text = fs.readFileSync('./txt/input.txt', 'utf-8');
console.log(text);
```

* Here is the console log-

![](assets/Pasted%20image%2020231129192535.png)
# Writing text to the file (Synchronous way ).

```js
//writeSileSync() used for write a file
//need to pass 'writing text file path' and 'content' as parameters
fs.writeSileSync('./txt/output.txt',`Hi this is I write ${text}`);
```
