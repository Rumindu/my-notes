* Text input field & Event listener (**onChangeText**)

* Adding Event Listener as <u>**anonymous function**</u>
```js
import React, { useState } from 'react';
import { StyleSheet, Text, View, TextInput } from 'react-native';

export default function App() {
  const [name, setName] = useState('shaun');
  const [age, setAge] = useState('30');

  return (
    <View style={styles.container}>

      <Text>Enter name:</Text>
      <TextInput 
        placeholder='e.g. John Doe' 
        style={styles.input}
        //Adding Event Listener as anonymous function
        onChangeText={(value) => setName(value)} />

      <Text>Enter age:</Text>
      <TextInput 
        placeholder='e.g. 99' 
        style={styles.input}
        //Adding Event Listener as anonymous function
        onChangeText={(value) => setAge(value)} />

      <Text style={styles.result}>name: {name}, age: {age}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  input: {
    borderWidth: 1,
    borderColor: '#777',
    padding: 8,
    margin: 10,
    width: 200,
  }
});
```
* example for Event Listner calling external function
```js
import React, { useState } from 'react';
import { StyleSheet, Text, View, TextInput } from 'react-native';

export default function App() {
  const [name, setName] = useState('shaun');
  const [age, setAge] = useState('30');

  //external function
  const typing = (value) => {
    setName(value);
  }

  return (
    <View style={styles.container}>

      <Text>Enter name:</Text>
      <TextInput 
        placeholder='e.g. John Doe' 
        style={styles.input}
        //Adding Event Listner with external function
        onChangeText={typing} />

      <Text>Enter age:</Text>
      <TextInput 
        placeholder='e.g. 99' 
        style={styles.input}
        //Adding Event Listner with anonymous function
        onChangeText={(value) => setAge(value)} />

      <Text style={styles.result}>name: {name}, age: {age}</Text>
    </View>
  );
}
```
* Adding different types of props into **TextInput**
1. `multiline` prop - To add lines when type enter
```js
<TextInput
        multiline
        placeholder='e.g. John Doe' 
        style={styles.input}
        onChangeText={(value) => setName(value)} />
```
<img src='./images/Screenshot 2023-09-17 192014.png'>
<br>

2. `keyboardType='numeric'` 
```js
 <TextInput 
        placeholder='e.g. 99' 
        keyboardType='numeric'
        style={styles.input}
        //Adding Event Listner with anonymous function
        onChangeText={(value) => setAge(value)} />
```
**props athara , demmoth weradi**

<img src='./images/Screenshot 2023-09-17 192537.png\'>
<br>
* More about TextInput props

https://reactnative.dev/docs/textinput