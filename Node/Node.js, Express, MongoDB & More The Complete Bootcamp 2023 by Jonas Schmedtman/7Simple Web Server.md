# Simple web server

* for that we need another module call `http`
  ```js
  const http = require('http');
  ```
  * in ordered to built a server
	  1. create a server
	  2. run server
	  
* Creating a server
 ```js
 const server=http.createServer((req, res) => {
   res.end('Hello from the server!');
 })
```

* starting server
  ```js
  server.listen(8000, '127.0.0.1',()=>{
    console.log('Listening to requests on port 8000');
 })
  ```
* normally when we compile the code and exit. But here program is running until we terminate it using `ctrl + c`.
* It happen something called **event loop**
* Once we enter `127.0.0.1:8000` in browser adders bar we can see the message
![](./assets/Pasted%20image%2020231218184601.png)

[Source code](https://github.com/Rumindu/work-Node.js-Jonas-Schmedtman/blob/main/2%20-%20Introduction%20to%20Nodejs%20and%20NPM/2SimpleWebServer.js)
