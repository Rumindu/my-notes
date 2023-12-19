# Simple routing
* Routing is implementing deferent actions for deferent URLS.
* for advanced routing we use **express** frame work.
* for simple routing we need built in node module called `url`. but for this session we are just require it only. we only need `http` module
```js
const http = require('http');
const url = require('url');

const server=http.createServer((req, res) => {
  console.log(req.url);
   res.end('Hello from the server!');
 })

server.listen(8000, '127.0.0.1',()=>{
  console.log('Listening to requests on port 8000');
 })
```
![](./assets/Pasted%20image%2020231219121623.png)
****Output***
![](./assets/Pasted%20image%2020231219120854.png)
* Once we create request through the browser we can see requested url and /favicon.ico. this favicon.ico request is generate by browser. and here we get empty url because we aren't passing any value.

![](./assets/Pasted%20image%2020231219121231.png)
![](./assets/Pasted%20image%2020231219121311.png)

## Simple routing implementation

```js
const http = require('http');
const url = require('url');

const server=http.createServer((req, res) => {
  const pathName = req.url;
    if(pathName === '/' || pathName === '/overview'){
      res.end('This is the OVERVIEW');
    }else if(pathName === '/product'){
      res.end('This is the PRODUCT');
    }
 })

server.listen(8000, '127.0.0.1',()=>{
    console.log('Listening to requests on port 8000');
 })

```
![](./assets/Pasted%20image%2020231219142541.png)

* If we request something else other than /overview and /products, server doesn't know what to do. So browser is just spinning.
* To prevent that just need to add else part
  ```js
  const server=http.createServer((req, res) => {
  const pathName = req.url;
    if(pathName === '/' || pathName === '/overview'){
      res.end('This is the OVERVIEW');
    }else if(pathName === '/product'){
      res.end('This is the PRODUCT');
    }
    else{
      res.end('Page not found!');
    }
 })
  ```
  ![](./assets/Pasted%20image%2020231219143335.png)
## Setting up http status code

* If the page isn't fund status code is `404` . to send it as response we use `res.writeHead()` function.
```js
const server=http.createServer((req, res) => {
  const pathName = req.url;
    if(pathName === '/' || pathName === '/overview'){
      res.end('This is the OVERVIEW');
    }else if(pathName === '/product'){
      res.end('This is the PRODUCT');
    }
    else{
      res.writeHead(404);
      res.end('Page not found!');
    }
 })
```
* We can see this status code in the development tools-> network tab
![](./assets/Pasted%20image%2020231219144844.png)

* By default if the page is available `200` status code will send

## Setup header
* HTTP header is a piece of information about the response that we are sending back.
* **==Always need to set up headers before sending response==**
  ```js
  res.writeHead(404,{
          'Content-type':'text/html',//browser is expecting some html
          'my-own-header':'hello-world'//custom header
        });
        res.end('<h1>Page not found!</h1>');
  ```

![](./assets/Pasted%20image%2020231219145727.png)

[Source codes](https://github.com/Rumindu/work-Node.js-Jonas-Schmedtman/blob/main/2%20-%20Introduction%20to%20Nodejs%20and%20NPM/3SimpleRouting.js)
