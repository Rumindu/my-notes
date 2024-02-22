* At '3stateUsingReacthook.md' we add **OnPress** event listener to the 'Button' component.
* But we can't pass 'Style' prop in to 'button' component.
* We can't attach event listener props like 'OnPress' to Component like `<Text>`
* So we can use `<TouchableOpacity>` component to apply 'Style' and 'OnPress' props.
* We can surround what ever component want to touchable using `<TouchableOpacity>` component

ex-
```js
<TouchableOpacity onPress={() => pressHandler(item.id)}>
  <Text style={styles.item}>{item.name}</Text>
</TouchableOpacity>
```
* Here `<Text>` is surrounded by  `TouchableOpacity`

```js
import React, { useState } from 'react';
import { StyleSheet, Text, View, FlatList, TouchableOpacity } from 'react-native';

export default function App() {
  const [people, setPeople] = useState([
    { name: 'shaun', id: '1' },
    { name: 'yoshi', id: '2' },
    { name: 'mario', id: '3' },
    { name: 'luigi', id: '4' },
    { name: 'peach', id: '5' },
    { name: 'toad', id: '6' },
    { name: 'bowser', id: '7' },
  ]);

  // when we press relevant box we can see relevant id in console
  const pressHandler = (id) => {
    console.log(id);
  };

  return (
    <View style={styles.container}>

      <FlatList 
        numColumns={2}
        keyExtractor={(item) => item.id} 
        data={people} 
        renderItem={({ item }) => (
          <TouchableOpacity onPress={() => pressHandler(item.id)}>
            <Text style={styles.item}>{item.name}</Text>
          </TouchableOpacity>
        )}
      />

    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: 40,
    paddingHorizontal: 20,
    backgroundColor: '#fff',
  },
  item: {
    flex: 1,
    marginHorizontal: 10,
    marginTop: 24,
    padding: 30,
    backgroundColor: 'pink',
    fontSize: 24,
  },
});
```
<img src="./images/Screenshot 2023-09-19 101516.png">
<img src="./images/Screenshot 2023-09-19 101535.png">

* **How to set When click on item item will be no longer there**
* using `filter` method
```js
import React, { useState } from 'react';
import { StyleSheet, Text, View, FlatList, TouchableOpacity } from 'react-native';

export default function App() {
  const [people, setPeople] = useState([
    { name: 'shaun', id: '1' },
    { name: 'yoshi', id: '2' },
    { name: 'mario', id: '3' },
    { name: 'luigi', id: '4' },
    { name: 'peach', id: '5' },
    { name: 'toad', id: '6' },
    { name: 'bowser', id: '7' },
  ]);

  const pressHandler = (id) => {
    console.log(id);
    setPeople((prevPeople) => {
      console.log(prevPeople);
      return prevPeople.filter(person => person.id  != id);
    });
    console.log(people);
  };

  return (
    <View style={styles.container}>

      <FlatList 
        numColumns={2}
        keyExtractor={(item) => item.id} 
        data={people} 
        renderItem={({ item }) => (
          <TouchableOpacity onPress={() => pressHandler(item.id)}>
            <Text style={styles.item}>{item.name}</Text>
          </TouchableOpacity>
        )}
      />

    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: 40,
    paddingHorizontal: 20,
    backgroundColor: '#fff',
  },
  item: {
    flex: 1,
    marginHorizontal: 10,
    marginTop: 24,
    padding: 30,
    backgroundColor: 'pink',
    fontSize: 24,
  },
});

```
<img src='./images/Screenshot 2023-09-19 111157.png'>

* After click 1st tab

<img src='./images/Screenshot 2023-09-19 111212.png'>
<br>
<br>
These are console logs of arrays
<img src='./images/Screenshot 2023-09-19 111236.png'>

* Here we can see using 'useState' and 'filter' existing list is changing
