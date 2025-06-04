## Learn React Native in Y Minutes

React Native is a JavaScript framework for building native mobile applications for iOS and Android. It allows developers to use the React library, along with native platform capabilities, to create a truly native user interface and performance while sharing a significant portion of the codebase across platforms.

### Core Concepts & Syntax

#### 1. Project Setup (Expo CLI & React Native CLI)

There are two main ways to set up a React Native project:

*   **Expo CLI:** A managed framework that simplifies development. Great for getting started quickly.
    ```bash
    # Install Expo CLI (if you haven't already)
    npm install -g expo-cli

    # Create a new project
    expo init MyReactNativeApp

    # Navigate into the project directory
    cd MyReactNativeApp

    # Start the development server
    npm start 
    # or
    expo start
    ```
    Expo Go app on your phone can then scan the QR code to run the app.

*   **React Native CLI:** Offers more flexibility and control, especially when you need to integrate custom native modules.
    ```bash
    # Install React Native CLI (if you haven't already)
    # (Ensure you have Node.js, Watchman, JDK, and Android Studio/Xcode installed)
    npm install -g react-native-cli

    # Create a new project
    react-native init MyReactNativeApp

    # Navigate into the project directory
    cd MyReactNativeApp

    # Start the development server for Android
    react-native run-android

    # Start the development server for iOS (on macOS)
    react-native run-ios
    ```

#### 2. Components: The Building Blocks

React Native UIs are built using components, similar to React for the web. React Native provides a set of built-in components that map to native UI widgets.

*   **Core Components:**
    *   `View`: The most fundamental component for building UI. It's a container that supports layout with flexbox, style, some touch handling, and accessibility controls. Think of it like a `<div>` in web development.
    *   `Text`: For displaying text.
    *   `Image`: For displaying images.
    *   `TextInput`: For user input.
    *   `ScrollView`: A generic scrolling container.
    *   `FlatList`: For rendering simple, flat lists. More performant for long lists.
    *   `SectionList`: For rendering sectioned lists.
    *   `Button`: A basic button component.
    *   `TouchableOpacity`, `TouchableHighlight`, `Pressable`: More customizable touch-responding components.

*   **Example: A Simple Component**
    ```javascript
    // App.js (or any component file)
    import React from 'react';
    import { StyleSheet, Text, View, Button, Alert } from 'react-native';

    export default function App() {
      const handlePress = () => {
        Alert.alert('Button Pressed!', 'You tapped the button.');
      };

      return (
        <View style={styles.container}>
          <Text style={styles.title}>Hello, React Native!</Text>
          <Text>This is a basic React Native app.</Text>
          <Button title="Press Me" onPress={handlePress} />
        </View>
      );
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1, // Takes up the full screen
        justifyContent: 'center', // Centers children vertically
        alignItems: 'center', // Centers children horizontally
        backgroundColor: '#f5fcff',
      },
      title: {
        fontSize: 24,
        fontWeight: 'bold',
        marginVertical: 10, // equivalent to marginTop and marginBottom
      },
    });
    ```

#### 3. Styling

Styling in React Native is done using JavaScript. You create `StyleSheet` objects. Properties are similar to CSS, but often use camelCase (e.g., `backgroundColor` instead of `background-color`).

*   **Creating Styles:**
    ```javascript
    import { StyleSheet } from 'react-native';

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        padding: 20,
        backgroundColor: 'white',
      },
      text: {
        fontSize: 16,
        color: 'blue',
      },
      // ... more styles
    });
    ```
*   **Applying Styles:**
    ```javascript
    <View style={styles.container}>
      <Text style={styles.text}>Styled Text</Text>
      <Text style={{ color: 'red', fontSize: 18 }}>Inline Styled Text</Text> 
      {/* Inline styles are also possible but less maintainable for complex styles */}
    </View>
    ```

#### 4. Layout with Flexbox

React Native uses Flexbox for layout by default on `View` components. It works similarly to CSS Flexbox, but with some differences (e.g., `flexDirection` defaults to `column` instead of `row`).

*   **Key Flexbox Properties:**
    *   `flex`: (number) Defines how an item should grow or shrink to fit the available space. `flex: 1` makes a component fill available space.
    *   `flexDirection`: (`row`, `column`, `row-reverse`, `column-reverse`) Defines the primary axis of layout. Default is `column`.
    *   `justifyContent`: (`flex-start`, `flex-end`, `center`, `space-between`, `space-around`, `space-evenly`) Aligns children along the primary axis.
    *   `alignItems`: (`flex-start`, `flex-end`, `center`, `stretch`, `baseline`) Aligns children along the secondary (cross) axis.
    *   `alignSelf`: Same as `alignItems` but for a single child.
    *   `padding`, `margin`: Similar to CSS. Can be `padding`, `paddingVertical`, `paddingHorizontal`, `paddingTop`, etc.

*   **Example: Flexbox Layout**
    ```javascript
    // In your component's render method
    // <View style={styles.layoutContainer}>
    //   <View style={styles.box1}><Text>Box 1</Text></View>
    //   <View style={styles.box2}><Text>Box 2</Text></View>
    //   <View style={styles.box3}><Text>Box 3</Text></View>
    // </View>

    // In your StyleSheet
    const styles = StyleSheet.create({
      layoutContainer: {
        flex: 1,
        flexDirection: 'row', // Arrange children horizontally
        justifyContent: 'space-around', // Distribute space around children
        alignItems: 'center', // Center children vertically in the row
        backgroundColor: 'lightgrey',
        paddingTop: 50, // Ensure content is visible below status bar
      },
      box1: {
        width: 80,
        height: 80,
        backgroundColor: 'skyblue',
        justifyContent: 'center',
        alignItems: 'center',
      },
      box2: {
        width: 80,
        height: 80,
        backgroundColor: 'lightgreen',
        justifyContent: 'center',
        alignItems: 'center',
      },
      box3: {
        width: 80,
        height: 80,
        backgroundColor: 'pink',
        justifyContent: 'center',
        alignItems: 'center',
      },
    });
    ```

#### 5. Handling User Input (Props & State)

React Native uses React's concepts of `props` (properties passed from parent to child) and `state` (data managed within a component that can change over time).

*   **Props:** Read-only data passed to components.
    ```javascript
    // Greeting.js
    import React from 'react';
    import { Text } from 'react-native';

    const Greeting = (props) => {
      return <Text>Hello, {props.name}!</Text>;
    };

    export default Greeting;

    // App.js
    // import Greeting from './Greeting';
    // <Greeting name="Sarah" /> 
    ```

*   **State:** Mutable data that triggers re-renders when updated.
    ```javascript
    import React, { useState } from 'react';
    import { View, Text, TextInput, Button, StyleSheet } from 'react-native';

    export default function NameInput() {
      const [name, setName] = useState(''); // Initialize state 'name' as an empty string
      const [submittedName, setSubmittedName] = useState('');

      const handleSubmit = () => {
        setSubmittedName(name);
      };

      return (
        <View style={styles.inputContainer}>
          <TextInput
            style={styles.input}
            placeholder="Enter your name"
            value={name} // Controlled component: value is tied to state
            onChangeText={setName} // Update state when text changes
          />
          <Button title="Submit" onPress={handleSubmit} />
          {submittedName ? <Text>Hello, {submittedName}!</Text> : null}
        </View>
      );
    }

    const styles = StyleSheet.create({
      inputContainer: {
        padding: 20,
      },
      input: {
        height: 40,
        borderColor: 'gray',
        borderWidth: 1,
        marginBottom: 10,
        paddingHorizontal: 8,
      },
    });
    ```

#### 6. Navigation

For multi-screen applications, you'll need a navigation library. `React Navigation` is the most popular solution.

*   **Installation (Example for Stack Navigation):**
    ```bash
    npm install @react-navigation/native @react-navigation/stack
    expo install react-native-screens react-native-safe-area-context # If using Expo
    # or for bare React Native projects:
    # npm install react-native-screens react-native-safe-area-context 
    # cd ios && pod install # For iOS
    ```

*   **Basic Stack Navigator Example:**
    ```javascript
    // App.js
    import React from 'react';
    import { View, Text, Button, StyleSheet } from 'react-native';
    import { NavigationContainer } from '@react-navigation/native';
    import { createStackNavigator } from '@react-navigation/stack';

    function HomeScreen({ navigation }) {
      return (
        <View style={styles.screen}>
          <Text>Home Screen</Text>
          <Button
            title="Go to Details"
            onPress={() => navigation.navigate('Details', { itemId: 86, otherParam: 'anything' })}
          />
        </View>
      );
    }

    function DetailsScreen({ route, navigation }) {
      const { itemId, otherParam } = route.params; // Access passed params
      return (
        <View style={styles.screen}>
          <Text>Details Screen</Text>
          <Text>Item ID: {JSON.stringify(itemId)}</Text>
          <Text>Other Param: {JSON.stringify(otherParam)}</Text>
          <Button title="Go to Details... again" onPress={() => navigation.push('Details', { itemId: Math.floor(Math.random() * 100) })} />
          <Button title="Go to Home" onPress={() => navigation.navigate('Home')} />
          <Button title="Go back" onPress={() => navigation.goBack()} />
        </View>
      );
    }

    const Stack = createStackNavigator();

    export default function App() {
      return (
        <NavigationContainer>
          <Stack.Navigator initialRouteName="Home">
            <Stack.Screen name="Home" component={HomeScreen} options={{ title: 'Overview' }} />
            <Stack.Screen name="Details" component={DetailsScreen} />
          </Stack.Navigator>
        </NavigationContainer>
      );
    }

    const styles = StyleSheet.create({
      screen: { flex: 1, alignItems: 'center', justifyContent: 'center' },
    });
    ```

#### 7. Platform-Specific Code

Sometimes you need to write different code for iOS and Android.

*   **Platform Module:**
    ```javascript
    import { Platform, StyleSheet } from 'react-native';

    const styles = StyleSheet.create({
      container: {
        paddingTop: Platform.OS === 'ios' ? 20 : 0, // Add padding only for iOS status bar
        backgroundColor: Platform.select({
          ios: 'silver',
          android: 'green',
          default: 'white' // For other platforms or web if using Expo for web
        }),
      },
    });
    ```
*   **File Extensions:**
    You can create files like `MyComponent.ios.js` and `MyComponent.android.js`. React Native will automatically pick the correct one.
    ```javascript
    // MyComponent.ios.js
    // import { Text } from 'react-native';
    // const MyComponent = () => <Text>This is for iOS</Text>;
    // export default MyComponent;

    // MyComponent.android.js
    // import { Text } from 'react-native';
    // const MyComponent = () => <Text>This is for Android</Text>;
    // export default MyComponent;

    // Then import it normally:
    // import MyComponent from './MyComponent';
    ```

#### 8. Fetching Data (Networking)

Use the `fetch` API (same as in web browsers) or libraries like `axios`.

```javascript
import React, { useEffect, useState } from 'react';
import { View, Text, FlatList, ActivityIndicator, StyleSheet } from 'react-native';

export default function DataFetcher() {
  const [isLoading, setLoading] = useState(true);
  const [data, setData] = useState([]);

  const fetchData = async () => {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/posts?_limit=5');
      const json = await response.json();
      setData(json);
    } catch (error) {
      console.error(error);
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    fetchData();
  }, []); // Empty dependency array means this runs once on mount

  return (
    <View style={styles.fetchContainer}>
      {isLoading ? (
        <ActivityIndicator size="large" color="#0000ff" />
      ) : (
        <FlatList
          data={data}
          keyExtractor={({ id }) => id.toString()}
          renderItem={({ item }) => (
            <View style={styles.item}>
              <Text style={styles.itemTitle}>{item.title}</Text>
            </View>
          )}
        />
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  fetchContainer: {
    flex: 1,
    padding: 20,
  },
  item: {
    padding: 10,
    borderBottomWidth: 1,
    borderBottomColor: '#cccccc',
  },
  itemTitle: {
    fontSize: 16,
  },
});
```

### Where to Go Next?

*   **Official React Native Documentation:** [https://reactnative.dev/docs/getting-started](https://reactnative.dev/docs/getting-started)
*   **Expo Documentation:** [https://docs.expo.dev/](https://docs.expo.dev/)
*   **React Navigation Documentation:** [https://reactnavigation.org/](https://reactnavigation.org/)

This tour provides a glimpse into the core aspects of React Native. Happy coding!

--- 