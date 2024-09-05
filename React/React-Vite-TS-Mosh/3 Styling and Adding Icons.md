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


# CSS Modules
-  In vanilla CSS, we may encounter conflicts if the same CSS classes are defined in multiple files