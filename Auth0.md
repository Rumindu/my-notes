# Auth 0

- Is a third party authentication provider.
- Custom tenant domain isn't available for the free plane, 

## Implementing Auth 0 for React-node full stack app

- [You tube link from Mafia Codes](https://www.youtube.com/watch?v=GGGjnBkN8xk

### Front-end
#### Setup front-end side in auth 0 dashboard side

1. Goes to the application -> application tab
2. In create new application choose single page web application.
3. In there settings->Basic information
	1. Domain == tenant name(can't change)
	2. Client Id
	3. Client secret
4. Settings ->Application URIs
	1. Allowed callback URLs -> provide application running url and port (http://localhost:3000)
	2. Allowed Logout URLs -> When the user is logout where to redirect (http://localhost:3000)
	3. Allowed web origins -> (http://localhost:3000)
5. Then save the changes

#### Front-end Dependencies 
- @auth0/auth0-react
- axios
#### Front-end code
- From @auth0/auth0-react library we need to get `<Auth0Provider>` component and need to pass values for below props
	- Domain == tenant name
	- ClientID -> From the settings->Basic information
	- audience == secret -> From API settings(Back-ends auth0 configuration)
	- redirect uri -> Callback url
-  We can appear login page as a pop up `{loginWithPopup}`or redirect to the another page `{loginWithRedirect}`

### Back end
#### Setup back-end side in auth 0 dashboard side
1. Goes to the application -> APIs tab
2. Create ApI
3. Here in the pop, 
	1. provide the Name 
	2. Identifier (it can be any thing normally providing url pf API- (http://localhost:4000))
	3. Choose algorithm
### Back-end code
- For back end we need to pass value for the `audience` when calling `auth` function. `audience` ===  `Identifier` in API settings
---
## Call back URL
- Once the user is successfully login where to the redirect.

## How to get sample access token for API development
- use [Auth0 Authentication API Debugger](https://dev-tpbo7d8k7mbc3rnr.us.webtask.run/auth0-authentication-api-debugger) extension in the Auth0 dash board.
- You tube tutorial [What is the Audience?](https://youtu.be/o_MuvVF9pY4).

## Auth 0 with Node js

- More info [The Complete Guide to Node.js User Authentication with Auth0](https://auth0.com/blog/complete-guide-to-nodejs-express-user-authentication/) and [The Complete Guide to React User Authentication with Auth0](https://auth0.com/blog/complete-guide-to-react-user-authentication/)
- Implementing auth0 for  React TS + node TS [Hello World Full-Stack Security:React/TypeScript + Express.js/TypeScript](https://developer.auth0.com/resources/code-samples/full-stack/hello-world/basic-access-control/spa/react-typescript/express-typescript)

* Once we login auth0 will return 2 tokens
	1. id token
	2. Access token

1. id Token
	* ![](assets/Pasted%20image%2020240129095743.png)
	
	* This is the content of ***id*** token
	* here ==sub== property is a unique identifier for user inside the Auth0
	* When we store other data relevant to the user we store under ==sub_id== as user id in db.

2. Access token
 ---

- High-level architecture. 
 ![](Internship/Daily-notes/assets/Pasted%20image%2020240222160710.png)
