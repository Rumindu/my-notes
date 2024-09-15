# Type Script Setup 
## Mosh Tutorial- Execute TS code
### 1. Compile TS to JS and run it on node
1. Compile TS file using `tsc file_name.ts`. Then it will create `file_name.js`
2. `node file_name.js` to run the JS code.
### 2. using `npm` package called `ts-node`
1. `npm init -y` for create basic `package.json` file.
2. `npm i -D ts-node` install `ts-node` as development dependency.
3. Go to `package.json` and add new start script
	``` json 
		"scripts": {
			"start": "ts-node index.ts"
		},
	```
4. then run `npm start`
- Here we couldn't see compiled JS file physically. It is located on memory. 
### 3.  Install `ts-node` globally. (not much recommend)
1. In the bash terminal `npm i -g ts-node` to install `ts node` globally
2. Then `ts-node index.ts`
- You can find the way to run PowerShell once u put error message on copilot chat . hint `Set-ExecutionPolicy Restricted` to `Set-ExecutionPolicy RemoteSigned` in PowerShell with admin
	To resolve this issue, you need to change the execution policy for PowerShell to allow running scripts. Here are the steps:

	1. Open PowerShell as an administrator.
	2. Run the following command to set the execution policy to `RemoteSigned`:
		`Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`
  3. When prompted, type `Y` and press Enter to confirm.
	After setting the execution policy, you should be able to run `pnpm` commands without encountering the security error.

	If you want to revert the execution policy to its default setting after running your scripts, you can use:
	`Set-ExecutionPolicy Restricted -Scope CurrentUser`
	This will disable script execution again.

---
## Academind tutorial initiate setup

- Install ts globally `npm install -g typescript`
- Compile ts file to create js file `tsc filename.ts`
- By default Even having ts type error js file will be create from above command.
- For this academind project, he use development server called "lite-server". To run this we need to run `npm start` on terminal.
- So then it will automatically refresh the browser after occure changes on js file. ==not in TS file==. There fore we need to manually compile ts file using `tsc` command