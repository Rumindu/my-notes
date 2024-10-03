[Short note](assets/Styling%20Components(Summary).pdf)
- There we are going to explore various techniques of styling components.
	1. Vanilla CSS
	2. CSS modules
	3. CSS in JS
	4. Using CSS library
# Vanilla CSS
- With vanilla CSS, we write our component styles in a separate CSS file and import it into the component file.
- Remove bootstrap import from `main.tsx`
- Create a `ListGroup.css` at component folder next to `ListGroup.tsx`.
- Here we aren't put `ListGroup.css` on separate folder called 'Styles'. Because `ListGroup.css` and `ListGroup.tsx` are highly related. We should things should be next to each other according to **Cohesion** concepts in software engineering.
- If we sperate these two files and put the CSS file in a sperate folder like Styles folder, tomorrow if you want to take this component and use it for different project we have to go to 2 different folders and cherry  pick different files. So it will mitigate component reusability.
- Next level of folder structure is add a new folder called `ListGroup`in the Component folder. And this folder have all the materials to built this component
``` shell 
components
└───ListGroup
        ListGroup.css
        ListGroup.tsx  
```
- In above folder structure we will get little bit ugly code when importing the `ListGroup` component.
	``` tsx 
	//App.tsx
	//repeating word ListGroup
	import ListGroup from "./components/ListGroup/ListGroup";
	```
- We can solve this problem creating `index.tsx` file inside the `ListGroup` folder
``` shell 
components
└───ListGroup
            index.ts
            ListGroup.css
            ListGroup.tsx
```

``` ts 
//index.ts
import ListGroup from "./ListGroup";
export default ListGroup;
```
- Now when we importing `ListGroup` component just enough for  include "ListGroup" folder name. Because by default if we don't provide a file and only refer a folder, the compiler will look for a file called `index`
	``` tsx 
	//App.tsx
	import ListGroup from "./components/ListGroup";
	```
	
	``` tsx 
	//ListGroup.tsx
	import ./ListGroup.css';

	function ListGroup() {
		return <ul className="list-group"></ul>
	}
 	```
 	[Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/40ca2418b59b6876e732a86520fb644c04e297af/src)
---

# CSS Modules
- In vanilla CSS, we may encounter clashes if the same CSS classes are defined in multiple files. As an example we declared another list-group class on `App.css` and importing it to `App.tsx` then set background to Blue. Apart from this in `ListGroup.css` we set background to Green. 
	![](assets/Pasted%20image%2020240907131901.png)
	[Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/c7866963bc00d35790a79c19d243d664bedd92e4/src)
- Here we can see a CSS clash. This is the problem CSS modules try to solve.
- A CSS module is a CSS file in, which all class names are scoped locally, just like a JavaScript module. So they allow us to use the same CSS class name in different files, without worrying about name clashes.
- First we need to rename file to convert existing CSS file to CSS module. Format is `"FileName".modules.css`
  - ex- `ListGroup.css ---> ListGroup.modules.css`
- Then need to update style sheet reference in the `ListGroup.tsx`
	- In plain CSS - `import './ListGroup.css'`
	- In CSS modules - `import styles from './ListGroup.modules.css'`
- Referencing CSS module is just like importing component/object.
- Now `styles` is just a regular JS object that has all CSS classes defined in `ListGroup.modules.css`. Therefore every CSS class defined here is going to be a part of `styles` object.
- Apply CSS class name within `{ }` instead of `" "` like [rendering dynamic content](1%20Introduction#Create%20dynamic%20content%20using%20JSX). 
  ![](assets/Pasted%20image%2020240908145939.png)
- Now we are getting compiler error due to having hyphen(`-`) in CSS class name. In JS `-` isn't valid property name therefore we couldn't access this property using using dot(`.`) notation instead we have to use square bracket.
	``` tsx 
	//ListGroup.tsx
	<ul className={styles['list-group']}>
	```
	[Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/ba54fe8bfb1e490f37a1e838df8464a09fcf7672/src/components/ListGroup)
- So now we couldn't see any CSS clashes. How does it work?
  ![](assets/Pasted%20image%2020240908153129.png)
  - So here we couldn't see `list-group` class name. It's encoded. As part of bundling application Vite takes all the CSS modules and create unique class. So it will prevent CSS clashing.
- CSS modules with this `[ ]` is a little bit ugly. So usually when using CSS modules, prefer to use **Camal** notation. So instead of using `-` we use the Camal notation.
  ``` css 
	/*ListGroup.module.css*/
	.listGroup{
		list-style: none;
		padding: 0%;
	}
	```
- With that we can access this CSS class just like a regular JS object.
  ``` tsx 
	//ListGroup.tsx  
	<ul className={styles.listGroup}>
	```
	[Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/2c40597b4f6d89b83dc8a60513449b5e5543fc2d/src/components/ListGroup/ListGroup.tsx)
- what if we want to add multiple CSS classes to the element
  ``` tsx 
	//ListGroup.tsx 
	<ul className={[styles.listGroup, styles.container].join(" ")}>
	```
	[Source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/tree/eb831acb2dffc5b3fc4064c17f7b6b490c93e247/src/components/ListGroup)
- why `join` ?
  ![](assets/Pasted%20image%2020240908215548.png)
---

# [**React Icons in a React Application**](https://react-icons.github.io/react-icons/)

1. **Install React Icons**
    
   - Install the library using the terminal:`npm install react-icons@4.7.1`
        
2. **Explore React Icons**
    
   - Visit the React Icons website to browse available icons.
   - React Icons is collection of multiple icon libraries, such as:
     - **Ant Design Icons** (prefix: `Ai`)
     - **Bootstrap Icons** (prefix: `Bs`)
     - **Box Icons** (prefix: `Bi`)
     - etc.
3. **Copy Icon**
	![](assets/Pasted%20image%2020241002135710.png)
	![](assets/Pasted%20image%2020241002135342.png)
	![](assets/Pasted%20image%2020241002135754.png)
    
   - Find the icon you want, then click to copy its component name.
  
4. **Import Icon**
    
   - In your React component (e.g., `App.js`), import the icon:
		``` tsx 
		import { BsCalendar } from "react-icons/bs";
		```
        
5. **Use the Icon**
    
   - Use the imported icon as a regular React component:
		``` tsx 
		const App = () => {
			return (
				<div><BsCalendar/></div>
			)
		```
		[source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/608da8a11a8726e3ff526a06aabd0376bfbdd416/src/App.tsx)

        
6. **Customize Icon**
    
   - Icons can be customized by adjusting props such as size, color,...:
		``` tsx 
		<BsCalendar color="red" size="40"/>
		```
		[source code](https://github.com/Rumindu/codeWithMosh-react-course-part1/blob/f73220c5e124a84381a6a4f49d6a649ba2bb7ba1/src/App.tsx)