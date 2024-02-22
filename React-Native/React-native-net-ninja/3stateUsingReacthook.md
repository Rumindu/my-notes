* <h2>Using 'UseState' hook.</h2>
* adding "OnPress" prop in to "button component"
```js
import React, { useState } from 'react'; //importing useState react hook
import { StyleSheet, Text, View, Button } from 'react-native';

export default function App() {

  //adding state
  const [denName, clickKaramaNama] = useState('Rumindu');//name is assigning value "Rumindu"

  const clickKaranna = () => {
    clickKaramaNama('Kavishka'); //updating name 
  };
  return (
    <View style={styles.container}>
      {/*Displaying name */}
      <Text>My name is {denName}</Text>
      <View>
        {/*onPress calling 'clickKaranna' function */}
        <Button title='Click Karanna' onPress={clickKaranna} />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent:'center',
  },
});
```
<hr>

* There can be multiple state
* Passing object 
```js
import React, { useState } from 'react'; //importing useState react hook
import { StyleSheet, Text, View, Button } from 'react-native';

export default function App() {

  //adding state
  const [denName, clickKaramaNama] = useState('Rumindu');//name is assigning value "Rumindu"

  //adding state
  //passing object intend of string
  const [person, setPerson] = useState({ name: 'mario', age: 40 });

  const clickKaranna = () => {
    clickKaramaNama('Kavishka'); //updating name
    setPerson({ name: 'Kavindu', age: 50 });
  };
  return (
    <View style={styles.container}>
      {/*Displaying */}
      <Text>My name is {denName}</Text>
      <Text>His name is {person.name} and his age is {person.age}</Text>
      <View>
        {/*onPress calling 'clickKaranna' function */}
        <Button title='Click Karanna' onPress={clickKaranna} />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent:'center',
  },
});

```
* Befor click
<img src="./images/Screenshot 2023-09-16 134812.png">

* After click
<img src="./images/Screenshot 2023-09-16 134820.png">