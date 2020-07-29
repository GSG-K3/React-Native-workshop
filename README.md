# React-Native-workshop
Introduction For React Native 

## React-Native 

React Native is a JavaScript framework Allow you to writes real, natively rendering mobile applications for iOS and Android ,based on React.
You can create code just once and use it to power both their iOS and Android apps. This translates to huge time and resource savings. ,React Native has the ability to render APIs in Objective-C (for iOS) or Java (for Android),your application will render using “bridge” to become real mobile UI components,and will look and feel like any other mobile application,your React Native apps can access platform features like the phone camera, or the user’s location.

![Test Image 1](https://www.netguru.com/hs-fs/hubfs/image10-Jul-03-2020-11-20-54-82-AM.png?width=1600&name=image10-Jul-03-2020-11-20-54-82-AM.png)

Now we can start building our first React Native App ,to do that you can follow the steps below:
### 1.Install React Native :
Assuming that you not familiar with mobile development,you will need Node 12 LTS to use npm to install the Expo CLI command line utility:
```
$ npm install -g expo-cli
```
Then run the following commands to create a new React Native project :
```
$ expo init myFirstNative
$ cd myFirstNative
$ code .
```

### 2.let's modify it
Open App.js in your text editor and edit some lines:

```js
import React from 'react';
import { StyleSheet, Text, View, Button, Alert } from 'react-native';

export default function App() {

return (
    <View style={styles.container}>
      <Text style={styles.title}>This Is My First React Native App</Text>
      <View style={styles.buttonContainer}>
      <Button
      title="click me"
      color="#841584"
      onPress={() => Alert.alert('Good Job Freinds')}
      />
      </View>
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
  title: {
    fontSize:25,
  },
  buttonContainer:{
    padding: 10
  },
  });
```
You can take alook at [React Native Components and API](https://reactnative.dev/docs/components-and-apis) If you want to add more elements to your app, and to learn more about iOS and Android-specific components.

run the following command in your terminal
```
$ npm start
```
Now If you want to see your changes....there is two ways to do it:

- Install the Expo client app on your iOS or Android phone and connect to the same wireless network as your computer. On Android, use the Expo app to scan the QR code from your terminal to open your project. On iOS, use the built-in QR code scanner of the Camera app.
- you can launch your app on an [Android Virtual Device](https://docs.expo.io/workflow/android-studio-emulator/) by running npm run android, or on the [iOS Simulator](https://docs.expo.io/workflow/ios-simulator/) by running npm run ios (macOS only).

You can use the first way to save time.


### Resources:
- [expo](https://expo.io/learn)
- [React-native setup](https://reactnative.dev/docs/environment-setup#docsNav)
