* **Flat List** - Like `<ScrollView>` but Flat List is more optimize than ScrollView>
1. **Display List item using `<FlatList>`**
* There is considerable difference between `<ScrollView>` and `<Flat List>`. In `<Flat List>` we aren't using array **map** function. We are passing several types of props into <FlatList> component.

**<FlatList
        {/* passing props */}
        data={people} 
        renderItem={({ item }) => ( 
          <Text style={styles.item}>{item.name}</Text>
        )}
      />** 
```js
import React, { useState } from 'react';
import { StyleSheet, Text, View, FlatList } from 'react-native';

export default function App() {
  const [people, setPeople] = useState([
    { name: 'shaun',key: '1' },
    { name: 'yoshi',key: '2' },
    { name: 'mario',key: '3' },
    { name: 'luigi',key: '4' },
    { name: 'peach',key: '5' },
    { name: 'toad',key: '6' },
    { name: 'bowser',key: '7' },
  ]);

  return (
    <View style={styles.container}>
      <FlatList
        {/* passing props */}
        data={people} 
        renderItem={({ item }) => ( 
          <Text style={styles.item}>{item.name}</Text>
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
<img src="./images/Screenshot 2023-09-18 153403.png">
<br>

* flat list look at 'key' property. Each item must have 'key property'

2. **When list has 'id' property intend of 'key' property**

**keyExtractor={(item) => item.id}**
```js
import React, { useState } from 'react';
import { StyleSheet, Text, View, FlatList } from 'react-native';

export default function App() {
  const [people, setPeople] = useState([
    { name: 'shaun',id: '1' },
    { name: 'yoshi',id: '2' },
    { name: 'mario',id: '3' },
    { name: 'luigi',id: '4' },
    { name: 'peach',id: '5' },
    { name: 'toad',id: '6' },
    { name: 'bowser',id: '7' },
  ]);

  return (
    <View style={styles.container}>
      {/* passing keyExtractor prop */} 
      <FlatList
        keyExtractor={(item) => item.id}
        data={people} 
        renderItem={({ item }) => ( 
          <Text style={styles.item}>{item.name}</Text>
        )}
      />

    </View>
  );
}
```
3. **Adding numColumns prop**
```js
<FlatList
        numColumns={2}
        keyExtractor={(item) => item.id}
        data={people} 
        renderItem={({ item }) => ( 
          <Text style={styles.item}>{item.name}</Text>
        )}
      />
```

<img src='./images/Screenshot 2023-09-18 184944.png'>