#This is a React Native crash course by academind
<img src="./Screenshot 2023-08-03 213808.png">    

`npm install -g expo—cli`

*meka gahanna onee command line eke VS code eke terminal eke gehuwama case
*mekedi expo install wenne globally
<br>
`expo init RNCourse`
<!-- <img src="./Screenshot 2023-08-03 214418.png"> -->

* Meka gahannath onee cmd eke.Vs eke terminal eke epe. Here creating new file called RNCourse and create project here. Methana sub folder nethuwa project eke create karaganna one nam `expo init .`
* meka run karain passe cmd eke ena option walin **blank project** eke thoraganna
* After this command type <b>npm start</b> for start this project

**Some files in folder structure**
1. assert - will be use for store images
2. app.json - configure some settings and behavior
3. App.js- only real code file to start this project

we are using expo go app to preview our project
<hr>
<img src="./Screenshot 2023-08-04 120948.png">

Differ between mobile and browser. They don't suport html elements. html wala tiyena `div` eke wage preform karanne `View` kiyana eke.
 
* This is the Root component of React native. Any other component must go throw this component

<img src="./Screenshot 2023-08-04 114758.png">

Here we can create our own componenet combining build in react-native componenet. For more deteils about React native pre build component- https://reactnative.dev/docs/components-and-apis
<img src="./Screenshot 2023-08-04 105959.png">



##### Styling React Native Apps
* react native doesn't have CSS
* applying inline style using Props or Style sheet object in the code  
<img src="./Screenshot 2023-08-04 120027.png">
<hr>

* App is the root component in React
* we can't put text without having `Text` component(tag).
```JavaScript
//error will occur due to not having <Text>
export default function App() {
  return (
    <View style={styles.container}>
      Another piece of text
    </View>
  );
```
<img src="./Screenshot 2023-08-04 121742.png"> 

* error message- Text string must be render within in a text compoennt
<br> 
* html wala div eke ethule kelinma text gahanna puluwan unata meke view eke ethule nikanma text gahanna bee. text component eke onee
* `Text` is a component - To display text
* `View` - Hold and layout other components. it'snot able display text.
* `View` component can contain multiple child component.
```JavaScript
 export default function App() {
  return (
    <View style={styles.container}>
      <Text>Another piece of text</Text>
      <Text>Another piece of text123</Text>
      <StatusBar style="auto" />
    </View>
  );
}
```
* we can have nested `View`
```JavaScript
export default function App() {
  return (
    <View style={styles.container}>
      <View>                            //nested View
      <Text>Another piece of text</Text>
      </View>
      <Text>Another piece of text</Text>
      <Text>Another piece of text123</Text>
      <StatusBar style="auto" />
    </View>
  );
}
```

* Add a button
<img src="./Screenshot 2023-08-04 125454.png">
* It is n't only relevant for `button` for use any component first we need to import it. ex- view, TestInput, StyleSheet
```JavaScript
import { StyleSheet, Text, View, Button } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <Text>Another piece</Text>
      <Button title='This is a button'/>  //Html wala wage neme button eke meka self closing element ekek
    </View>
    
  );
```
<img src="./Screenshot 2023-08-04 135113.png">
<hr>
# Styling React Native Apps
* There is no CSS
* There is 2 way 2 add styles form the passing style object throw the prop
  1.inline Styles
  2.StyleSheet Objects
* To Apply style we can use `style prop` It isn't support all the element but it support `view` and `Text` component
## inline Styles

``` JavaScript
      <Text style={{
          margin: 16, //Here margin is 15px
          borderWidth: 3, //applying a boarder with density is 1px
          borderColor: "red", // here we can apply hexcode or rgb values
          padding: 16
        }}
      >
        Another piece
      </Text>
  ````
  <img src="./Screenshot 2023-08-04 135606.png">

## StyleSheet Objects


```JavaScript
import { StyleSheet, Text, View, Button } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <Text
        style={styles.styleRumindu} //refering new property
      >
        Another piece
      </Text>
      <Button title='This is a button' />
    </View>
  );
}

//Here we already have a style object so we create a new property in the object to get styles
const styles = StyleSheet.create({ 
  container: {
    flex: 1,
    backgroundColor: "yellow",
    alignItems: "center",
    justifyContent: "center",
  },
  //create new property
  styleRumindu: {
    margin: 16,
    borderWidth: 3,
    borderColor: "red",
    padding: 16,
  },
});














