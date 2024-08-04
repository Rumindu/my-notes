# Setting up express project in TS
- initiate package.json file using `npm init -y`
- Install below packages
  1. `npm i express`
  2. `npm i -d typescript @types/node @types/express` Here even ts install globally we install ts because when the device is change it doesn't need to contain ts globally installed.
  3.  `tsc --init` To create TS compiler configuration file.
- create `index.ts` file
  ``` ts 
  //index.ts
  import  express from 'express';
  const app = express();
  app.listen(3000, () => {
    console.log('Server is running on port 3000');
  });
  ```
-  to run this application we can use `ts-node` but the problem is every time we made a change we have to stop server and restart it. So the issue is Nodemon.
- It watch the files and every time we made a change it restart the server.
- `npm i -D nodemon` Install Nodemon as development dependency.
- Current Nodemon suport ts-node. so Nodemon will compile ts with Ts-node.
- Change start script on `package.json`
  ``` json
  "start": "nodemon index.ts"
  ```