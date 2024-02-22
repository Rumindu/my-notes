**Output List of Data**
```js
import React, { useState } from "react";
import { StyleSheet, Text, View, FlatList } from "react-native";

export default function App() {
  // Object which contains list of items
  // When we output the list of items, we need to use the key property to identify each item uniquely.
  const [people, setPeople] = useState([
    { name: "shaun", key: "1" },
    { name: "yoshi", key: "2" },
    { name: "mario", key: "3" },
    { name: "luigi", key: "4" },
    { name: "peach", key: "5" },
    { name: "toad", key: "6" },
    { name: "boser", key: "6" },
  ]);

  // mapping array
  const travel = people.map((item) => {
    return (
      <View>
        <Text>{item.name}</Text>
      </View>
    );
  });

  return (
    <View style={styles.container}>
      {/* calling function */}
      {travel}
    </View>
  )
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: 40,
    paddingHorizontal: 20,
    backgroundColor: "#fff",
  },
});
```
* about example using an anonymous function.
```js
 return (
    <View style={styles.container}>
      {people.map((item) => {
        return (
      <View>
        <Text>{item.name}</Text>
      </View>
    )
  })}
    </View>
  )
```
here some error is occurring
<img src='./images/Screenshot 2023-09-18 143254.png'>

* Error- Each child in a list should have a unique "key" prop.

**To prevent this error** providing a unique key prop for each item in the list.
* ***That's why we provide "key" in list***
```js
{people.map((item) => {
  return (
    <View key={item.key}>
      <Text>{item.name}</Text>
    </View>
  );
})}
```
<hr>

* Adding some styles and Scroll view
```js
import React, { useState } from "react";
import { StyleSheet, Text, View, ScrollView } from "react-native";

export default function App() {
  const [people, setPeople] = useState([
    { name: "shaun", key: "1" },
    { name: "yoshi", key: "2" },
    { name: "mario", key: "3" },
    { name: "luigi", key: "4" },
    { name: "peach", key: "5" },
    { name: "toad", key: "6" },
    { name: "boser", key: "7" },
  ]);
  return (
    <ScrollView>
      <View style={styles.container}>
        {people.map((item) => {
          return (
        <View key={item.key}>
          <Text style={styles.item}>{item.name}</Text>
        </View>
      )
    })}
      </View>
    </ScrollView>
  )
}
const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: 40,
    paddingHorizontal: 20,
    backgroundColor: "#fff",
  },
  item: {
    marginTop: 24,
    padding: 30,
    backgroundColor: 'pink',
    fontSize: 24,
  }
});

```
<br>
<img src="./images/Screenshot 2023-09-18 153403.png">

we can write this function like this
```js
{people.map(item => (
        <View key={item.key}>
          <Text style={styles.item}>{item.name}</Text>
        </View>
      )
    )}
```
