## Getting a data from JSON file
```js
const http = require("http");
const fs = require("fs");

//here we are using synchronous method because we want to read the file only once when the server starts
//__dirname is representing current file direction
const data=fs.readFileSync(`${__dirname}/data.json`, "utf-8");
//create a javascript object from the json file
const dataObj=JSON.parse(data);

const server = http.createServer((req, res) => {
  const pathName = req.url;
  if (pathName === "/" || pathName === "/overview") {
    res.end("This is the OVERVIEW");
  } else if (pathName === "/product") {
    res.end("This is the PRODUCT");
    
    //simple API
  } else if (pathName === "/api") {
    res.writeHead(200, { "Content-type": "application/json" });//browser is expecting a json
      res.end(data);
  } else {
    res.writeHead(404, {
      "Content-type": "text/html", 
      "my-own-header": "hello-world",
    });
    res.end("<h1>Page not found!</h1>");
  }
});

server.listen(8000, "127.0.0.1", () => {
  console.log("Listening to requests on port 8000");
});
```